from datetime import datetime

print("\n" + "="*70)
print("ВЫПОЛНЕНИЕ ЗАПРОСОВ К БАЗЕ ДАННЫХ")
print("="*70)

# ============ ЗАПРОС 1: ЗАКАЗЫ ЗА СЕГОДНЯ ============
print("\n1️⃣ ЗАКАЗЫ ЗА СЕГОДНЯ:")
print("-"*70)

query1 = """
SELECT 
    o.id AS order_id,
    u.name AS customer,
    GROUP_CONCAT(p.name || ' (' || oi.quantity || ' шт.)', ', ') AS products,
    ROUND(SUM(oi.quantity * p.price), 2) AS total,
    o.status
FROM orders o
JOIN users u ON o.user_id = u.id
JOIN order_items oi ON o.id = oi.order_id
JOIN products p ON oi.product_id = p.id
WHERE DATE(o.order_date) = DATE('now')
GROUP BY o.id
"""

cursor.execute(query1)
results1 = cursor.fetchall()

if results1:
    for row in results1:
        print(f"  Заказ #{row[0]} | {row[1]} | Товары: {row[2]} | Итого: ${row[3]} | Статус: {row[4]}")
else:
    print("  ❌ Заказов за сегодня нет")

# ============ ЗАПРОС 2: ПОПУЛЯРНЫЙ ТОВАР МЕСЯЦА ============
print("\n2️⃣ САМЫЙ ПОПУЛЯРНЫЙ ТОВАР МЕСЯЦА:")
print("-"*70)

query2 = """
SELECT 
    p.name AS product,
    SUM(oi.quantity) AS total_sold,
    ROUND(SUM(oi.quantity * p.price), 2) AS revenue
FROM products p
JOIN order_items oi ON p.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE strftime('%Y-%m', o.order_date) = strftime('%Y-%m', 'now')
GROUP BY p.id
ORDER BY total_sold DESC
LIMIT 1
"""

cursor.execute(query2)
result2 = cursor.fetchone()

if result2:
    print(f"  📦 {result2[0]} | Продано: {result2[1]} шт. | Выручка: ${result2[2]}")
else:
    print("  ❌ Нет данных за текущий месяц")

# ============ ЗАПРОС 3: ЛУЧШИЙ ПОСТАВЩИК ============
print("\n3️⃣ ПОСТАВЩИК С МАКСИМАЛЬНОЙ СУММОЙ ПОСТАВОК:")
print("-"*70)

query3 = """
SELECT 
    s.name AS supplier,
    ROUND(SUM(oi.quantity * p.price), 2) AS total_amount,
    COUNT(DISTINCT oi.order_id) AS orders_count
FROM suppliers s
JOIN products p ON s.id = p.supplier_id
JOIN order_items oi ON p.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE strftime('%Y', o.order_date) = strftime('%Y', 'now')
GROUP BY s.id
ORDER BY total_amount DESC
LIMIT 1
"""

cursor.execute(query3)
result3 = cursor.fetchone()

if result3:
    print(f"  🏆 {result3[0]} | Сумма поставок: ${result3[1]} | Кол-во заказов: {result3[2]}")
else:
    print("  ❌ Нет данных за текущий год")

print("\n" + "="*70)
print("✅ ВСЕ ЗАПРОСЫ ВЫПОЛНЕНЫ")
print("="*70)

conn.close()
