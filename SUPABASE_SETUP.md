# Supabase 数据库设置指南

## 1. 创建数据表

请在 Supabase 控制台中执行以下 SQL 语句来创建数据表：

```sql
-- 创建用户数据表
CREATE TABLE user_data (
    id BIGSERIAL PRIMARY KEY,
    user_id TEXT NOT NULL,
    device_id TEXT NOT NULL,
    data JSONB NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 为 user_id 创建唯一索引（每个用户只有一条记录）
CREATE UNIQUE INDEX idx_user_data_user_id ON user_data(user_id);

-- 为 updated_at 创建索引以提高查询性能
CREATE INDEX idx_user_data_updated_at ON user_data(updated_at);

-- 启用行级安全策略（RLS）
ALTER TABLE user_data ENABLE ROW LEVEL SECURITY;

-- 创建策略：允许所有人读取和写入（因为使用的是匿名密钥）
CREATE POLICY "允许所有操作" ON user_data
    FOR ALL
    USING (true)
    WITH CHECK (true);
```

## 2. 执行步骤

1. 登录 Supabase 控制台：https://app.supabase.com
2. 选择你的项目：`vryhcjblxglvewohkdkf`
3. 点击左侧菜单的 "SQL Editor"
4. 点击 "New Query"
5. 将上面的 SQL 代码粘贴到编辑器中
6. 点击 "Run" 按钮执行

## 3. 验证

执行完成后，你可以：
1. 点击左侧菜单的 "Table Editor"
2. 查看是否出现了 `user_data` 表
3. 表结构应该包含以下字段：
   - id (bigint)
   - user_id (text)
   - device_id (text)
   - data (jsonb)
   - updated_at (timestamp)
   - created_at (timestamp)

## 4. 功能说明

### 数据同步机制
- **自动同步**：每次保存数据时，会自动同步到云端
- **手动同步**：点击右上角的云端同步按钮可以手动同步
- **冲突处理**：手动同步时会比较本地和云端的更新时间，使用最新的数据

### 多设备使用
1. 在第一台设备上使用时，会提示输入昵称（如 "Alan"）
2. 在其他设备上使用时，输入相同的昵称即可同步数据
3. 每台设备会自动生成唯一的设备ID

### 数据安全
- 数据存储在 Supabase 云端（PostgreSQL 数据库）
- 同时在本地 localStorage 保留备份
- 即使云端同步失败，本地数据也不会丢失

## 5. 故障排除

### 如果同步失败
1. 检查网络连接
2. 确认 Supabase 项目是否正常运行
3. 查看浏览器控制台的错误信息
4. 点击同步按钮重试

### 如果数据不一致
1. 点击右上角的云端同步按钮
2. 系统会自动选择最新的数据
3. 如果需要，可以使用"数据导出"功能备份当前数据

## 6. 注意事项

- 首次使用时输入的昵称很重要，请记住它
- 如果忘记昵称，可以在浏览器控制台输入 `localStorage.getItem('userId')` 查看
- 建议定期使用"数据导出"功能备份数据
