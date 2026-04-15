# Добавляем тестовые заказы за сегодняшнюю дату
from datetime import date

today = date.today().isoformat()

# Добавляем нового пользователя
cursor.execute("INSERT INTO users(name, email, password, phone) VALUES(?,?,?,?)", 
               ("Тестовый", "test@mail.com", "test123", "999999"))
new_user_id = cursor.lastrowid

# Добавляем заказ за сегодня
cursor.execute("INSERT INTO orders(user_id, employee_id, order_date, status) VALUES(?,?,?,?)",
               (new_user_id, 1, today, "processing"))
new_order_id = cursor.lastrowid

# Добавляем товар в заказ
cursor.execute("INSERT INTO order_items(order_id, product_id, quantity) VALUES(?,?,?)",
               (new_order_id, 1, 2))

# Добавляем платеж
cursor.execute("INSERT INTO payments(order_id, amount, payment_date, method) VALUES(?,?,?,?)",
               (new_order_id, 2400, today, "card"))

conn.commit()
print(f"\n✅ Добавлен тестовый заказ на сегодня ({today})")
