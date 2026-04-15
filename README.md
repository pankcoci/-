from datetime import datetime

# Добавляем реальные заказы за сегодня
today = datetime.now().strftime('%Y-%m-%d')

print(f"📅 Сегодня: {today}")

# Добавляем пользователя
cursor.execute("INSERT INTO users(name, email, password, phone) VALUES(?,?,?,?)", 
               ("Срочный Клиент", "urgent@mail.com", "fast123", "7777777"))
user_id = cursor.lastrowid

# Добавляем заказ
cursor.execute("INSERT INTO orders(user_id, employee_id, order_date, status) VALUES(?,?,?,?)",
               (user_id, 1, today, "processing"))
order_id = cursor.lastrowid

# Добавляем товары
cursor.execute("INSERT INTO order_items(order_id, product_id, quantity) VALUES(?,?,?)",
               (order_id, 1, 1))  # Ноутбук
cursor.execute("INSERT INTO order_items(order_id, product_id, quantity) VALUES(?,?,?)",
               (order_id, 3, 2))  # Мыши

# Добавляем платеж
cursor.execute("INSERT INTO payments(order_id, amount, payment_date, method) VALUES(?,?,?,?)",
               (order_id, 1250.00, today, "card"))

conn.commit()
print(f"✅ Добавлен заказ #{order_id} на сегодня!")
