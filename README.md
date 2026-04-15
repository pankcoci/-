# 1. Заказы за сегодня с ПРОДУКТАМИ
query1 = """
SELECT 
    o.id AS order_id,
    u.name AS user_name,
    GROUP_CONCAT(DISTINCT p.name, ', ') AS products,
    SUM(oi.quantity) AS total_items,
    ROUND(SUM(oi.quantity * p.price), 2) AS total_amount,
    o.order_date,
    o.status
FROM orders o
JOIN users u ON o.user_id = u.id
JOIN order_items oi ON o.id = oi.order_id
JOIN products p ON oi.product_id = p.id
WHERE DATE(o.order_date) = DATE('now')
GROUP BY o.id, u.name, o.order_date, o.status
"""
execute_query(query1, "Заказы за сегодня с продуктами")
