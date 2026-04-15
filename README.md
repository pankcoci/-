# После conn.commit() и до conn.close()

def execute_query(query, description):
    cursor.execute(query)
    results = cursor.fetchall()
    print(f"\n{'='*50}")
    print(f"{description}:")
    print(f"{'='*50}")
    for row in results:
        print(row)
    return results

# 1. Заказы за сегодня
query1 = """
SELECT 
    o.id AS order_id,
    u.name AS user_name,
    o.order_date,
    o.status
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE DATE(o.order_date) = DATE('now')
"""
execute_query(query1, "Заказы за сегодня")

# 2. Самый популярный товар месяца
query2 = """
SELECT 
    pr.name AS product_name,
    SUM(oi.quantity) AS total_sold
FROM products pr
JOIN order_items oi ON pr.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE strftime('%Y-%m', o.order_date) = strftime('%Y-%m', 'now')
GROUP BY pr.id
ORDER BY total_sold DESC
LIMIT 1
"""
execute_query(query2, "Самый популярный товар месяца")

# 3. Поставщик с максимальной суммой поставок
query3 = """
SELECT 
    s.name AS supplier_name,
    SUM(oi.quantity * pr.price) AS total_amount
FROM suppliers s
JOIN products pr ON s.id = pr.supplier_id
JOIN order_items oi ON pr.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE strftime('%Y', o.order_date) = strftime('%Y', 'now')
GROUP BY s.id
ORDER BY total_amount DESC
LIMIT 1
"""
execute_query(query3, "Поставщик с наибольшей суммой поставок")
