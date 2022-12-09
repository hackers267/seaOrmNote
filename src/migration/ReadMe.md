# 迁移

seaOrm提供了迁移命令，以方便数据库从开发环境到测试环境的迁移。

在迁移文件中，有两个命令：`up`和`down`。

### 表创建语句

在对表创建语句(TableCreateStatement)进行说明前，先看一下示例：
```rust
Table::create()
    .table(TableCustom::Table)
    .if_not_exists()
    .col(
        ColumnDef::new(TableCustom::Id)
        .string()
        .not_null()
        .primary_key(),
    )
    .col(ColumnDef::new(TableCustom::UserId).string().not_null())
    .col(ColumnDef::new(TableCustom::App).string().not_null())
    .col(ColumnDef::new(TableCustom::TableName).string().not_null())
    .to_owned(),
```

下面看一下具体的方法：
- .col 定义字段
- .if_not_exists 如果不存在表，则创建
- .collate 指定字符类型