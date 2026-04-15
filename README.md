# После conn.commit() и до conn.close()

def execute_query(query, description):
    cursor.execute(query)
    results = cursor.fetchall()
    print(f"\n{'='*50}")
    print(f"{description}:")
    print(f"{'='*50}")
    if results:
        for row in results:
            print(row)
    else:
        print("(нет данных)")
    return results

# 1. Заказы за сегодня (для тестовых данных используем 2025-01-27)
print("\n🔍 ПРИМЕЧАНИЕ: В тестовых данных даты из января 2025 года")
print("Для демонстрации используем дату 2025-01-27\n")

query1 = """
SELECT 
    o.id AS order_id,
    u.name AS user_name,
    u.email,
    o.order_date,
    o.status,
    SUM(p.amount) AS total_amount
FROM orders o
JOIN users u ON o.user_id = u.id
LEFT JOIN payments p ON o.id = p.order_id
WHERE DATE(o.order_date) = DATE('2025-01-27')  -- Заменили на конкретную дату
GROUP BY o.id, u.name, u.email, o.order_date, o.status
"""
execute_query(query1, "Заказы за 2025-01-27")

# 2. Самый популярный товар месяца (январь 2025)
query2 = """
SELECT 
    pr.id AS product_id,
    pr.name AS product_name,
    SUM(oi.quantity) AS total_quantity_sold,
    COUNT(DISTINCT o.id) AS number_of_orders
FROM products pr
JOIN order_items oi ON pr.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE o.order_date BETWEEN '2025-01-01' AND '2025-01-31'  -- Указали январь 2025
GROUP BY pr.id, pr.name
ORDER BY total_quantity_sold DESC
LIMIT 1
"""
execute_query(query2, "Самый популярный товар за январь 2025")

# 3. Поставщик с наибольшей суммой поставок в 2025 году
query3 = """
SELECT 
    s.id AS supplier_id,
    s.name AS supplier_name,
    s.phone,
    SUM(oi.quantity * pr.price) AS total_supply_amount,
    COUNT(DISTINCT oi.order_id) AS number_of_orders
FROM suppliers s
JOIN products pr ON s.id = pr.supplier_id
JOIN order_items oi ON pr.id = oi.product_id
JOIN orders o ON oi.order_id = o.id
WHERE strftime('%Y', o.order_date) = '2025'  -- Указали 2025 год
GROUP BY s.id, s.name, s.phone
ORDER BY total_supply_amount DESC
LIMIT 1
"""
execute_query(query3, "Поставщик с наибольшей суммой поставок в 2025 году")

conn.close()
print("\n✅ Запросы выполнены!")
