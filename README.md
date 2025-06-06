## -2 AGREGO EL SIGUIENTE PRODUCTO 

    db.products.insertOne({
        sku:"A101",
        name:"Figura Naruto Uzumaki",
        category: "Figuras",
        price: 120000,
        stock: 10,
        anime: "Naruto",
        rating: 4.8,
        tags: ["coleccionable", "resina", "edición especial"],
        provider: {
            name: "OtakuDistribuciones",
            country: "Japón"
        }
    })

## -3 AGREGO A TODOS LOS PRODUCTOS LAS SIGUIENTES PROPIEDADES 

    db.products.updateMany(
        {},
        {
		    $set:{
			    available: true,
			    origin: "Importado"
			
		    }
	    }
    )

## -4 REALIZO LAS SIGUIENTES ACTUALIZACIONES

# Producto con sku: A034, actualizar stock a 15

    db.products.updateOne(
        {sku :"A034"}, {$set: {stock: 15}}
    )   

# Producto con sku: A018, cambiar el country del provider a "Colombia".

    db.products.updateOne(
        {sku :"A018"}, {$set: {"provider.country": "Colombia"}}
    )

# ​Producto con sku: A059, agregar un nuevo tag: "oferta".

    db.products.updateOne(
        {sku :"A059"}, {$addToSet: {tags: "oferta"}}
    )

# Producto con sku: A012, agregar dos nuevos tags: "nuevo", "popular".

    db.products.updateOne(
        {sku :"A012"}, {$addToSet: {tags: {$each : ["nuevo","popular"]}}}
    )

# Producto con sku: A025, agregar los tags "descuento", "outlet".

    db.products.updateOne(
        {sku :"A025"}, {$addToSet: {tags: {$each : ["descuento","outlet"]}}}
    )

# Producto llamado "Camiseta Goku Ultra Instinct", cambiar el price a 45000.

    db.products.updateOne(
        {name :"Camiseta Goku Ultra Instinct"}, {$set: {price: 45000}}
    )

## -5 RENOMBRAR LA PROPIEDAD  ORIGIN A IMPORT_TYPE

    db.products.updateMany(
        {},
        {$rename: {origin: "import_type"}}
    )

## -6 CAMBIAR EL import_type a "Nacional" PARA LOS PRODUCTOS CUYO PROVEEDOR ESTE EN COLOMBIA

    db.products.updateMany(
        {"provider.country": "Colombia"},
        {$set : {import_type:"Nacional"}}
    )

## -7 CREAR LAS SIGUIENTES CONSULTAS

# Mostrar los productos de la categoría "Mangas"

    db.products.find(
        {category: "Mangas"}
    )

# Mostrar los productos que tienen un precio mayor a 50000

    db.products.find(
        {price: {$gt : 49999}}
    )

# Mostrar los productos que no son de la categoría "Figuras"

    db.products.find(
        {category: {$ne : "Figuras"}}
    )

# Mostrar el sku, name y tags de los productos que tienen calificación mayor a 4.5
    db.products.find(
        {rating: {$gt : 4.5}},
        {sku:1,name:1,tags:1}
    )

# Mostrar sku, name, y price de los productos con stock menor a 5.

    db.products.find(
        {rating: {$lt : 5}},
        {sku:1,name:1,price:1}
    )

## -8 ELIMINAR LA PROPIEDAD AVAILABLE DE TODOS LOS DOCUMENTOS 

    db.products.updateMany(
        {},
        {$unset : {available: ""}}
    )

## -9 ELIMINAR EL TAG "descuento" DEL PRODUCTO CON SKU: A025
    
    db.products.updateOne(
        {sku: "A025"},
        {$pull : {tags: "descuento"}}
    )

## -10 ELIMINAR EL TAG "nuevo" y "popular" DEL PRODUCTO CON SKU: A012

    db.products.updateOne(
        {sku: "A012"},
        {$pull : {tags: {$in:["nuevo","popular"]}}}
    )

##  -11 ELIMINAR EL PRODUCTO CON SKU: A043.

    db.products.deleteOne(
        {sku: "A043"}
    )


## -12 ELIMINAR TODOS LOS PRODUCTOS CON STOCK IGUAL A 0.
    db.products.deleteMany(
        {stock: 0}
    )