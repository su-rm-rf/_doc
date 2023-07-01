# 表结构
Category (
  id int,
  name: varchar,
  primary key (id)
)
Goods (
  id int,
  name: varchar,
  category_id int,
  primary key (id),
  constraint fkn foreign key (category_id) references Category (id)
)
User {
  id int,
  username varchar,
  password varchar,
  level int
}
Cart {
  id int,
  user int
}
Cart_Item {
  id int,
  goods_id int,
  amount int,
  cart_id int
}
Order {
  id int,
  user int
}
Order_Item {
  id int,
  goods_id int,
  amount int,
  order_id int
}

# dotenv配置全局变量
键值对，值只能是字符串类型

# MySQL数据库连接池
连接池：为了防止有大量请求同时对数据库进行访问，是一组预先分配的数据库连接，可以大幅提高响应速度

数据库连接次数过多

  const pool = mysql.createPool(config)
  pool.query(sql, params, (err, res, fields)=>{})

事务
  pool.getConnection()
    connect.begineTransaction
      connect.query(SQL)
        connect.rollback()
        connect.commit()
    connect.release()


# TypeORM
JoinColumn({ name: fkn }) 在从表中，把ManyToOne的Column映射到fkn上，数据库里合并成一个字段
JoinTable()

