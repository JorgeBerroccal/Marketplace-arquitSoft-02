# Arquitectura inicial del sistema

## Marketplace de productos para mascotas

## Diagrama de arquitectura

```mermaid
flowchart TD

    %% =========================
    %% ACTORES
    %% =========================
    subgraph ACTORES["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    %% =========================
    %% PRESENTACIÓN
    %% =========================
    subgraph PRESENTACION["PRESENTACIÓN"]
        Web["Aplicación Web"]
        API["API REST"]
    end

    %% =========================
    %% LÓGICA DE NEGOCIO
    %% =========================
    subgraph NEGOCIO["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    %% =========================
    %% DATOS
    %% =========================
    subgraph DATOS["DATOS"]
        BD["Base de datos"]
    end

    %% =========================
    %% SISTEMAS EXTERNOS
    %% =========================
    subgraph EXTERNOS["SISTEMAS EXTERNOS"]
        Pago["Pasarela de pago"]
        Facturacion["Servicio de Facturación"]
        Envio["Servicio de envío"]
        ERP["ERP"]
    end

    %% =========================
    %% FLUJO PRINCIPAL
    %% =========================
    Cliente --> Web
    Seller --> Web
    Admin --> Web

    Web --> API
    API --> Usuarios
    API --> Sellers
    API --> Catalogo
    API --> Carrito
    API --> Pedidos

    Usuarios --> BD
    Sellers --> BD
    Catalogo --> BD
    Carrito --> BD
    Pedidos --> BD

    %% =========================
    %% INTEGRACIONES EXTERNAS
    %% =========================
    Pedidos --> Pago
    Pedidos --> Facturacion
    Pedidos --> Envio
    Catalogo --> ERP
    ERP --> Catalogo

```

## Descripción

La arquitectura inicial se organiza en tres capas principales:

- **Presentación:** permite la interacción de los clientes, sellers y administradores mediante la aplicación web y la API REST.
- **Lógica de negocio:** contiene los módulos de usuarios, sellers, catálogo, carrito y pedidos, responsables de implementar las principales funcionalidades del Marketplace.
- **Datos:** contiene la base de datos utilizada para almacenar y consultar la información del sistema.

Además, la arquitectura contempla la integración con sistemas externos:

- **Pasarela de pago:** procesa los pagos de los pedidos.
- **Servicio de facturación:** genera los comprobantes de pago.
- **Servicio de envío:** gestiona la información relacionada con la entrega.
- **ERP:** proporciona información de productos y stock.