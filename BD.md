DROP DATABASE IF EXISTS ARTISAN_DB;

CREATE DATABASE IF NOT EXISTS ARTISAN_DB;

USE ARTISAN_DB;

CREATE TABLE User (
	user_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    password VARCHAR(128),
	name VARCHAR(50),
    surnames VARCHAR(50),
    telephone VARCHAR(15),
    description VARCHAR(255),
    image VARCHAR(255) NOT NULL
);


CREATE TABLE Artisan (
	artisan_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    password VARCHAR(128),
	name VARCHAR(50),
    surnames VARCHAR(50),
    telephone VARCHAR(15),
    description VARCHAR(255),
    image VARCHAR(255) NOT NULL
);

CREATE TABLE Category (
	category_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE Product (
	product_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    artisan_id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    image VARCHAR(100) NOT NULL,
    description TEXT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    category_id INT NOT NULL,
    creation_date DATE NOT NULL,
    sold BOOLEAN DEFAULT FALSE,
    user_id INT,
    buy_date DATE,
    visible BOOLEAN DEFAULT TRUE,
    FOREIGN KEY (artisan_id) REFERENCES Artisan(artisan_id),
    FOREIGN KEY (category_id) REFERENCES Category(category_id),
	FOREIGN KEY (user_id) REFERENCES User(user_id)
);

/*CREATE TABLE User_Product (
	artisan_id INT NOT NULL,
	user_id INT,
    product_id INT NOT NULL,
    creation_date DATE NOT NULL,
    buy_date DATE,
    FOREIGN KEY (artisan_id) REFERENCES Artisan(artisan_id),
    FOREIGN KEY (user_id) REFERENCES User(user_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);*/

CREATE TABLE Likes (
	id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	user_id INT,
    product_id INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES User(user_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);

CREATE TABLE Followers (
	id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	follower_id INT NOT NULL,
    following_id INT NOT NULL,
    FOREIGN KEY (follower_id) REFERENCES User(user_id),
    FOREIGN KEY (following_id) REFERENCES Artisan(artisan_id)
);

CREATE TABLE Chat_Room (
	room_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    product_id INT NOT NULL,
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);

CREATE TABLE Chat_Message (
	message_id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    room_id INT NOT NULL,
    user_id INT,
    artisan_id INT,
    timestamp TIMESTAMP NOT NULL,
    FOREIGN KEY (room_id) REFERENCES Chat_Room(room_id),
    FOREIGN KEY (user_id) REFERENCES User(user_id),
    FOREIGN KEY (artisan_id) REFERENCES Artisan(artisan_id)
);

USE ARTISAN_DB;
INSERT INTO User (username, email, password, name, surnames, telephone, description, image) VALUES
('julia21', 'julia.smith@example.com', 'julia2023', 'Julia', 'Smith', '+34 612 345 678', 'Apasionada del arte clásico y la pintura al óleo.', 'http://localhost:8080/images/users/1_User.jpg'),
('alex1985', 'alex.brown@example.com', 'alex1985pass', 'Alex', 'Brown', '+34 671 234 567', 'Amante de la fotografía y la edición digital.', 'http://localhost:8080/images/users/2_User.jpg'),
('laura78', 'laura.jones@example.com', 'laura78pass', 'Laura', 'Jones', '+34 645 678 901', 'Fanática de la escultura y el arte contemporáneo.', 'http://localhost:8080/images/users/3_User.jpg'),
('marioG', 'mario.garcia@example.com', 'marioGpass', 'Mario', 'García', '+34 600 123 456', 'Apasionado por la música y el diseño gráfico.', 'http://localhost:8080/images/users/4_User.jpg'),
('emilio_s', 'emilio.s@example.com', 'emilio2023', 'Emilio', 'Sánchez', '+34 666 987 654', 'Interesado en la arquitectura y el arte urbano.', 'http://localhost:8080/images/users/5_User.jpg'),
('anamaria', 'ana.maria@example.com', 'anamaria123', 'Ana', 'María', '+34 655 432 109', 'Apasionada de la danza y las artes escénicas.' , 'http://localhost:8080/images/users/6_User.jpg'),
('juan_89', 'juan89@example.com', 'juanito891', 'Juan', 'González', '+34 666 789 012', 'Amante de la literatura y la poesía.', 'http://localhost:8080/images/users/7_User.jpg'),
('marina91', 'marina91@example.com', 'marinaPass91', 'Marina', 'Fernández', '+34 600 888 777', 'Entusiasta de la moda y el diseño de moda.', 'http://localhost:8080/images/users/8_User.jpg'),
('carlos_p', 'carlos.perez@example.com', 'carlos123pass', 'Carlos', 'Pérez', '+34 601 234 567', 'Fanático del cine y el arte audiovisual.', 'http://localhost:8080/images/users/9_User.jpg'),
('elena1976', 'elena1976@example.com', 'elenita1976', 'Elena', 'Gómez', '+34 611 987 654', 'Amante de las artes plásticas y la creatividad.', 'http://localhost:8080/images/users/19_User.jpg');

INSERT INTO Artisan (username, email, password, name, surnames, telephone, description, image) VALUES
('juanmar', 'artesano1@example.com', 'juanmar', 'Juan', 'Martínez', '612345678', 'Artesano experto en cerámica y alfarería.', 'http://localhost:8080/images/artisans/2_Artisan.jpg'),
('marilo', 'artesano2@example.com', 'marilo', 'María', 'López', '633456789', 'Diseñadora de joyería hecha a mano.', 'http://localhost:8080/images/artisans/1_Artisan.jpg'),
('peregar', 'artesano3@example.com', 'peregar', 'Pedro', 'García', '644567890', 'Escultor especializado en mármol y piedra.', 'http://localhost:8080/images/artisans/5_Artisan.jpg'),
('larod', 'artesano4@example.com', 'larod', 'Laura', 'Rodríguez', '655678901', 'Tejedora creativa de textiles y tejidos.', 'http://localhost:8080/images/artisans/3_Artisan.jpg'),
('carfer', 'artesano5@example.com', 'carfer', 'Carlos', 'Fernández', '666789012', 'Pintor impresionista con estilo único.', 'http://localhost:8080/images/artisans/4_Artisan.jpg'),
('anaper', 'artesano6@example.com', 'anaper', 'Ana', 'Pérez', '677890123', 'Restauradora de arte con amplia experiencia.', 'http://localhost:8080/images/artisans/6_Artisan.jpg'),
('jagom', 'artesano7@example.com', 'jagom', 'Javier', 'Gómez', '688901234', 'Creador de esculturas en metal y hierro.', 'http://localhost:8080/images/artisans/7_Artisan.jpg'),
('sarara', 'artesano8@example.com', 'sarara', 'Sara', 'Ramírez', '699012345', 'Talladora de madera con habilidades únicas.', 'http://localhost:8080/images/artisans/8_Artisan.jpg'),
('alejern', 'artesano9@example.com', 'alejern', 'Alejandro', 'Hernández', '610123456', 'Artista cervecero y experto en cervezas artesanales.', 'http://localhost:8080/images/artisans/9_Artisan.jpg'),
('maritor', 'artesano10@example.com', 'maritor', 'Marina', 'Torres', '611234567', 'Creadora de piezas de cerámica inspiradas en la naturaleza.', 'http://localhost:8080/images/artisans/10_Artisan.jpg');


INSERT INTO Category (name) VALUES
('Muebles de madera'),
('Arte en cerámica'),
('Esculturas en metal'),
('Tejidos hechos a mano');


INSERT INTO Product (artisan_id, name, image, description, price, category_id, creation_date, visible) VALUES
(1, 'Mesa de comedor de roble', 'http://localhost:8080/images/product/9_Product.png', 'Mesa de comedor hecha a mano con roble macizo.', 499.99, 1, '2023-07-01', TRUE),
(2, 'Jarrón de cerámica decorativo', 'http://localhost:8080/images/product/2_Product.png', 'Jarrón artístico de cerámica pintado a mano.', 39.99, 2, '2023-07-05', TRUE),
(3, 'Escultura de metal abstracta', 'http://localhost:8080/images/product/7_Product.png', 'Escultura única de metal con diseño abstracto.', 199.99, 3, '2023-07-10', TRUE),
(4, 'Bufanda tejida a mano', 'http://localhost:8080/images/product/13_Product.jpg', 'Bufanda cálida y suave tejida a mano con lana de alpaca.', 29.99, 4, '2023-07-15', TRUE),
(5, 'Silla de madera de haya', 'http://localhost:8080/images/product/5_Product.png', 'Silla ergonómica hecha de madera de haya natural.', 129.99, 1, '2023-07-20', TRUE),
(6, 'Jarrón de cerámica pintada', 'http://localhost:8080/images/product/6_Product.png', 'Jarrón de cerámica hecha y pintada a mano con motivos florales.', 49.99, 2, '2023-07-25', TRUE),
(7, 'Escultura de metal geométrica', 'http://localhost:8080/images/product/3_Product.png', 'Escultura geométrica moderna hecha de metal.', 179.99, 3, '2023-07-30', TRUE),
(8, 'Manta de punto grueso', 'http://localhost:8080/images/product/4_Product.png', 'Manta acogedora tejida a mano con lana merina.', 79.99, 4, '2023-08-01', TRUE),
(9, 'Mesa auxiliar de madera de pino', 'http://localhost:8080/images/product/11_Product.jpg', 'Mesa auxiliar elegante hecha de pino tratado.', 89.99, 1, '2023-08-05', TRUE),
(10, 'Cuadro de cerámica esmaltada', 'http://localhost:8080/images/product/12_Product.jpg', 'Cuadro decorativo de cerámica esmaltada con diseño abstracto.', 59.99, 2, '2023-08-10', TRUE),
(1, 'Silla artesanal de nogal', 'http://localhost:8080/images/product/14_Product.png', 'Silla robusta y elegante hecha a mano con madera de nogal.', 139.99, 1, '2023-08-15', TRUE),
(1, 'Mesa de centro de cerezo', 'http://localhost:8080/images/product/15_Product.png', 'Mesa de centro artesanal fabricada con madera de cerezo.', 219.99, 1, '2023-08-20', TRUE),
(2, 'Mesa de noche de abedul', 'http://localhost:8080/images/product/16_Product.png', 'Mesa de noche de diseño simple y elegante, hecha con madera de abedul.', 99.99, 1, '2023-08-25', TRUE),
(2, 'Silla artesanal de fresno', 'http://localhost:8080/images/product/17_Product.png', 'Silla cómoda y duradera fabricada a mano con madera de fresno.', 134.99, 1, '2023-08-30', TRUE),
(2, 'Mueble de madera de roble', 'http://localhost:8080/images/product/1_Product.png', 'Mueble fabricada a mano con madera de roble.', 434.99, 1, '2023-08-30', TRUE),
(3, 'Mesa de escritorio de arce', 'http://localhost:8080/images/product/18_Product.png', 'Mesa de escritorio espaciosa y resistente, fabricada con madera de arce.', 249.99, 1, '2023-09-01', TRUE);


INSERT INTO Likes (user_id, product_id) VALUES
(2, 1),
(3, 2),
(1, 3),
(4, 5),
(2, 6),
(3, 8),
(5, 10);


INSERT INTO Followers (follower_id, following_id) VALUES
(1, 2),
(1, 3),
(2, 1),
(3, 1),
(4, 2),
(5, 3);


INSERT INTO Chat_Room (product_id) VALUES
(1),
(3),
(5),
(7),
(9);


INSERT INTO Chat_Message (room_id, user_id, artisan_id, timestamp) VALUES
(1, 2, 1, '2023-07-01 12:05:23'),
(1, 1, 1, '2023-07-01 12:10:15'),
(2, 3, 2, '2023-07-05 15:30:42'),
(2, 2, 2, '2023-07-05 16:00:20'),
(3, 5, 3, '2023-07-10 09:25:17'),
(3, 3, 3, '2023-07-10 09:30:05'),
(4, 7, 4, '2023-07-30 17:45:11'),
(5, 9, 5, '2023-08-05 10:55:30');
