import sqlite3

conn = sqlite3.connect("internet_shop.db")
cursor = conn.cursor()

cursor.execute("PRAGMA foreign_keys = ON")

# -------------------------
# УДАЛЯЕМ ТАБЛИЦЫ ЕСЛИ БЫЛИ
# -------------------------

cursor.execute("DROP TABLE IF EXISTS payments")
cursor.execute("DROP TABLE IF EXISTS order_items")
cursor.execute("DROP TABLE IF EXISTS orders")
cursor.execute("DROP TABLE IF EXISTS products")
cursor.execute("DROP TABLE IF EXISTS suppliers")
cursor.execute("DROP TABLE IF EXISTS employees")
cursor.execute("DROP TABLE IF EXISTS users")

# -------------------------
# USERS
# -------------------------

cursor.execute("""
CREATE TABLE users(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
email TEXT,
password TEXT,
phone TEXT
)
""")

# -------------------------
# EMPLOYEES
# -------------------------

cursor.execute("""
CREATE TABLE employees(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
position TEXT,
salary REAL
)
""")

# -------------------------
# SUPPLIERS
# -------------------------

cursor.execute("""
CREATE TABLE suppliers(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
phone TEXT
)
""")

# -------------------------
# PRODUCTS
# -------------------------

cursor.execute("""
CREATE TABLE products(
id INTEGER PRIMARY KEY AUTOINCREMENT,
name TEXT,
price REAL,
stock INTEGER,
supplier_id INTEGER,
FOREIGN KEY(supplier_id) REFERENCES suppliers(id)
)
""")

# -------------------------
# ORDERS
# -------------------------

cursor.execute("""
CREATE TABLE orders(
id INTEGER PRIMARY KEY AUTOINCREMENT,
user_id INTEGER,
employee_id INTEGER,
order_date TEXT,
status TEXT,
FOREIGN KEY(user_id) REFERENCES users(id),
FOREIGN KEY(employee_id) REFERENCES employees(id)
)
""")

# -------------------------
# ORDER ITEMS
# -------------------------

cursor.execute("""
CREATE TABLE order_items(
id INTEGER PRIMARY KEY AUTOINCREMENT,
order_id INTEGER,
product_id INTEGER,
quantity INTEGER,
FOREIGN KEY(order_id) REFERENCES orders(id),
FOREIGN KEY(product_id) REFERENCES products(id)
)
""")

# -------------------------
# PAYMENTS
# -------------------------

cursor.execute("""
CREATE TABLE payments(
id INTEGER PRIMARY KEY AUTOINCREMENT,
order_id INTEGER,
amount REAL,
payment_date TEXT,
method TEXT,
FOREIGN KEY(order_id) REFERENCES orders(id)
)
""")

conn.commit()

# -------------------------
# ЗАПОЛНЕНИЕ USERS
# -------------------------

users = [
("Алексей","alex@mail.com","pass1","111111"),
("Дмитрий","john@mail.com","pass2","222222"),
("Мария","maria@mail.com","pass3","333333"),
("Анна","anna@mail.com","pass4","444444"),
("Давид","david@mail.com","pass5","555555"),
("Екатерина","kate@mail.com","pass6","666666"),
("Роман","robert@mail.com","pass7","777777"),
("Кристина","chris@mail.com","pass8","888888"),
("Ольга","olga@mail.com","pass9","999999"),
("Тимур","tom@mail.com","pass10","000000")
]

cursor.executemany(
"INSERT INTO users(name,email,password,phone) VALUES(?,?,?,?)",
users
)

# -------------------------
# EMPLOYEES
# -------------------------

employees = [
("Тимофей","Менеджер",3000),
("Станислава","Продавец",2000),
("Надежда","Продавец",2100),
("Кристина","Помощник",1900),
("Михаил","Курьер",1800),
("Таисия","Директор отдела кадров",2400),
("Владимир","айти специалист",2800),
("Карина","Бухгалтер",2500),
("Никита","Кладовщик",1900),
("Дарья","Маркетинговый специалист",2600)
]

cursor.executemany(
"INSERT INTO employees(name,position,salary) VALUES(?,?,?)",
employees
)

# -------------------------
# SUPPLIERS
# -------------------------

suppliers = [
("TechSupply","111111"),
("GlobalTech","222222"),
("MegaElectro","333333"),
("DeviceWorld","444444"),
("FutureTech","555555"),
("SmartDevices","666666"),
("ElectroBase","777777"),
("DigitalHub","888888"),
("ComputerParts","999999"),
("TechStore","000000")
]

cursor.executemany(
"INSERT INTO suppliers(name,phone) VALUES(?,?)",
suppliers
)

# -------------------------
# PRODUCTS
# -------------------------

products = [
("Ноутбук",1200,10,1),
("Игровой ПК",2000,5,2),
("Мышь",25,100,3),
("Клавиатура",45,60,4),
("Монитор",300,20,5),
("Наушники",80,40,6),
("Микрофон",120,15,7),
("Веб-камера",60,25,8),
("USB-флеш-память",15,200,9),
("Офисный стул",150,10,10)
]

cursor.executemany(
"INSERT INTO products(name,price,stock,supplier_id) VALUES(?,?,?,?)",
products
)

# -------------------------
# ORDERS
# -------------------------

orders = [
(1,1,"2025-01-10","completed"),
(2,2,"2025-01-12","completed"),
(3,3,"2025-01-13","processing"),
(4,4,"2025-01-15","completed"),
(5,5,"2025-01-18","processing"),
(6,6,"2025-01-20","completed"),
(7,7,"2025-01-22","processing"),
(8,8,"2025-01-23","completed"),
(9,9,"2025-01-25","processing"),
(10,10,"2025-01-27","completed")
]

cursor.executemany(
"INSERT INTO orders(user_id,employee_id,order_date,status) VALUES(?,?,?,?)",
orders
)

# -------------------------
# ORDER ITEMS
# -------------------------

order_items = [
(1,1,1),
(2,2,2),
(3,3,1),
(4,4,1),
(5,5,3),
(6,6,2),
(7,7,1),
(8,8,2),
(9,9,5),
(10,10,1)
]

cursor.executemany(
"INSERT INTO order_items(order_id,product_id,quantity) VALUES(?,?,?)",
order_items
)

# -------------------------
# PAYMENTS
# -------------------------

payments = [
(1,1200,"2025-01-10","card"),
(2,2000,"2025-01-12","card"),
(3,25,"2025-01-13","cash"),
(4,45,"2025-01-15","card"),
(5,300,"2025-01-18","paypal"),
(6,80,"2025-01-20","card"),
(7,120,"2025-01-22","card"),
(8,60,"2025-01-23","cash"),
(9,15,"2025-01-25","card"),
(10,150,"2025-01-27","paypal")
]

cursor.executemany(
"INSERT INTO payments(order_id,amount,payment_date,method) VALUES(?,?,?,?)",
payments
)

conn.commit()

print("База данных создана.")

conn.close()
#запуск - python app.py 
#имеются таблицы таукие как:
# • users — пользователи
# • employees — сотрудники
# • suppliers — поставщики
# • products — товары
# • orders — заказы
# • order_items — товары в заказе / позиции заказа
# • payments — платежи 
