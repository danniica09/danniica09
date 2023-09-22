CREATE DATABASE Supermercado;
USE Supermercado;


CREATE TABLE supermercado.tipoProducto(
    idTipoProducto INT (18) not null,
    NombreTipoProducto VARCHAR(50)not null,
    primary key (idTipoProducto)
);
	insert into tipoProducto( idTipoProducto,NombreTipoProducto)
    values (1,'limpiesa'),(2,'granos');
    
CREATE TABLE Supermercado.inventario (
    idProducto INT (18) not null,
    Cantidad INT (18) not null,
    primary key  (idProducto) );
    
    insert into inventario(idProducto,Cantidad)
    values (15,50),(20,50);
    
    CREATE TABLE supermercado.Producto (
    idProducto INT (18) not null,
    idTipoProducto int (18)null default null,
    nombreProducto varchar(18)not null,
    valorVenta int (18) not null,
    Primary key (idProducto));
    
    alter TABLE Supermercado.`producto`
    add constraint idtipoproducto
		foreign key(idtipoProducto)
        references Supermercado.`tipoproducto`(idTipoProducto)
        on delete no action
        on update no action;
        
	  insert into producto(idProducto,idTipoProducto,nombreProducto,valorVenta)
      values (15,2,'frijoles',3000),(20,1,'jabon de baño',2000);
      
    CREATE TABLE supermercado.factura (
    numerofactura int not null auto_increment,
    idProducto int (18) not null,
	Cantidad int (18) null default null,
    fechaVenta datetime,
    primary key (numerofactura ));
    
      alter TABLE Supermercado.`factura`
    add constraint idproducto
		foreign key(idProducto)
        references Supermercado.`producto`(idProducto)
        on delete no action
        on update no action;
    
    insert into factura(idProducto,Cantidad,fechaVenta)values(20,3,now());
    insert into factura(idProducto,Cantidad,fechaVenta)values(3,6,now());
    


DELIMITER //
CREATE TRIGGER actualizar_inventario AFTER INSERT ON factura
FOR EACH ROW
BEGIN
    UPDATE inventario SET Cantidad = Cantidad - NEW.Cantidad
    WHERE idProducto = NEW.idProducto;
END;
//
DELIMITER ;

select * from inventario factura


DELIMITER //
CREATE TRIGGER actualizar_nombreProducto
AFTER INSERT ON producto
FOR EACH ROW
BEGIN
		UPDATE producto
		SET actualizar_nombreProducto =now() 
		WHERE nombreProducto = NEW.nombreProducto;
	
END;
//
DELIMITER ;
select * from PRODUCTO
