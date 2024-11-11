# TaskMate
Website quản lý công việc việc theo nhóm

## Chức năng
### Quản lý bảng (Board Management)
Tạo, chỉnh sửa, xóa bảng (board) cho từng dự án.
Mô tả bảng để cung cấp thông tin về dự án.
Chia sẻ bảng với các thành viên khác để làm việc nhóm.

### Thêm, chỉnh sửa, xóa danh sách (list) trong bảng.
- Đặt thứ tự cho các danh sách để phản ánh các giai đoạn công việc (như “To Do,” “In Progress,” “Done”).

### Quản lý thẻ (Card Management)
- Tạo, chỉnh sửa, xóa thẻ (card) trong danh sách để quản lý các nhiệm vụ cụ thể.
- Thêm mô tả chi tiết cho mỗi thẻ.
- Đặt thứ tự cho các thẻ trong danh sách để ưu tiên công việc.

### Quản lý người dùng (User Management)
- Đăng ký, đăng nhập người dùng.
- Quản lý hồ sơ người dùng, bao gồm thông tin cá nhân và ảnh đại diện.
- Quản lý phân quyền người dùng (Owner, Member, Viewer) trong bảng.

### Gán nhiệm vụ (Task Assignment)
- Gán thẻ cho các thành viên để quản lý trách nhiệm.
- Tích hợp thông báo cho thành viên khi được gán thẻ mới.

### Checklist
- Tạo checklist cho từng thẻ để chia nhỏ nhiệm vụ.
- Đánh dấu hoàn thành từng mục trong checklist.

### Nhãn và ưu tiên (Labels and Priority)
- Tạo các nhãn màu sắc khác nhau để phân loại nhiệm vụ.
- Đặt mức độ ưu tiên cho các thẻ.

### Ngày đến hạn và nhắc nhở (Due Dates and Reminders)
- Đặt ngày đến hạn cho từng thẻ.
- Tự động gửi thông báo hoặc nhắc nhở cho các nhiệm vụ gần đến hạn.

### Bình luận và thảo luận (Comments and Discussion)
- Cho phép người dùng thêm bình luận vào thẻ để trao đổi thông tin.
- Gửi thông báo cho các thành viên khi có bình luận mới.

### Tìm kiếm và lọc (Search and Filter)
- Tìm kiếm thẻ theo từ khóa.
- Lọc nhiệm vụ theo nhãn, ngày đến hạn, người gán, v.v.

### Lịch sử hoạt động (Activity Log)
- Ghi lại các hoạt động trên bảng để người dùng theo dõi thay đổi.
- Xem lại các hành động gần đây của từng thành viên trên bảng.

### Thông báo (Notifications)
- Thông báo khi có thay đổi trong bảng hoặc nhiệm vụ liên quan đến người dùng.
- Thông báo qua email hoặc qua ứng dụng.

## Công cụ và ngôn ngữ
### Công cụ ( IDE, TOOLS)
- **_IDE_**: Webstorm, Visual Studio Code
- **_Tools_**: Git, Github
### Cơ sở dữ liệu (Database): MySql
### Ngôn ngữ (Language): Typescript
### Thư viện (Framework/Library) :
- **Frontend** : ReactJS + ViteJs, Antd, Shadcn, Material UI, TailwindCSS
- **Backend** : NodeJs, ExpressJs, RestfulAPI, Sequelize, Swagger

## Mô hình cơ sở dữ liệu
### Các bảng chính và các cột

1. **Bảng `Users`**
   - `id`: PK, UUID hoặc Auto Increment
   - `name`: Tên người dùng
   - `email`: Email người dùng (duy nhất)
   - `password_hash`: Mật khẩu mã hóa
   - `profile_picture`: Ảnh đại diện (URL)
   - `created_at`: Ngày tạo tài khoản

2. **Bảng `Boards`**
   - `id`: PK, UUID hoặc Auto Increment
   - `name`: Tên bảng
   - `description`: Mô tả bảng
   - `created_by`: FK, tham chiếu tới `Users.id`
   - `created_at`: Ngày tạo bảng
   - `updated_at`: Ngày cập nhật cuối cùng

3. **Bảng `Board_Users`** (Quan hệ N-N giữa `Boards` và `Users`)
   - `board_id`: FK, tham chiếu tới `Boards.id`
   - `user_id`: FK, tham chiếu tới `Users.id`
   - `role`: Vai trò của người dùng trong bảng (Owner, Member, Viewer)
   - `added_at`: Ngày thêm người dùng vào bảng

4. **Bảng `Lists`**
   - `id`: PK, UUID hoặc Auto Increment
   - `name`: Tên danh sách
   - `position`: Vị trí trong bảng để xác định thứ tự
   - `board_id`: FK, tham chiếu tới `Boards.id`
   - `created_at`: Ngày tạo danh sách
   - `updated_at`: Ngày cập nhật cuối cùng

5. **Bảng `Cards`**
   - `id`: PK, UUID hoặc Auto Increment
   - `title`: Tiêu đề của thẻ
   - `description`: Mô tả chi tiết
   - `position`: Vị trí trong danh sách để sắp xếp
   - `due_date`: Ngày đến hạn của thẻ
   - `list_id`: FK, tham chiếu tới `Lists.id`
   - `created_at`: Ngày tạo thẻ
   - `updated_at`: Ngày cập nhật cuối cùng

6. **Bảng `Card_Assignees`** (Gán thẻ cho người dùng)
   - `card_id`: FK, tham chiếu tới `Cards.id`
   - `user_id`: FK, tham chiếu tới `Users.id`
   - `assigned_at`: Ngày gán thẻ cho người dùng

7. **Bảng `Labels`**
   - `id`: PK, UUID hoặc Auto Increment
   - `name`: Tên nhãn
   - `color`: Màu sắc nhãn
   - `board_id`: FK, tham chiếu tới `Boards.id`

8. **Bảng `Card_Labels`** (Quan hệ N-N giữa `Cards` và `Labels`)
   - `card_id`: FK, tham chiếu tới `Cards.id`
   - `label_id`: FK, tham chiếu tới `Labels.id`

9. **Bảng `Checklists`**
   - `id`: PK, UUID hoặc Auto Increment
   - `name`: Tên checklist
   - `card_id`: FK, tham chiếu tới `Cards.id`
   - `created_at`: Ngày tạo checklist

10. **Bảng `Checklist_Items`**
    - `id`: PK, UUID hoặc Auto Increment
    - `content`: Nội dung của mục checklist
    - `is_completed`: Trạng thái (hoàn thành hoặc chưa)
    - `checklist_id`: FK, tham chiếu tới `Checklists.id`

11. **Bảng `Comments`** (Bình luận trên thẻ)
    - `id`: PK, UUID hoặc Auto Increment
    - `content`: Nội dung bình luận
    - `user_id`: FK, tham chiếu tới `Users.id`
    - `card_id`: FK, tham chiếu tới `Cards.id`
    - `created_at`: Ngày đăng bình luận

12. **Bảng `Activity_Log`** (Lịch sử hoạt động)
    - `id`: PK, UUID hoặc Auto Increment
    - `description`: Mô tả hoạt động (ví dụ: "Người dùng X đã gán thẻ cho Y")
    - `user_id`: FK, tham chiếu tới `Users.id`
    - `board_id`: FK, tham chiếu tới `Boards.id`
    - `card_id`: FK, tham chiếu tới `Cards.id` (nếu hoạt động liên quan đến một thẻ cụ thể)
    - `created_at`: Ngày ghi nhận hoạt động

13. **Bảng `Notifications`**
    - `id`: PK, UUID hoặc Auto Increment
    - `user_id`: FK, tham chiếu tới `Users.id` (người nhận thông báo)
    - `message`: Nội dung thông báo
    - `is_read`: Trạng thái đọc của thông báo
    - `created_at`: Ngày gửi thông báo

### Mối quan hệ giữa các bảng chính

- Mỗi `Board` có thể có nhiều `List`.
- Mỗi `List` có thể có nhiều `Card`.
- Mỗi `Card` có thể có nhiều `Checklist`.
- Mỗi `Checklist` có thể có nhiều `Checklist_Item`.
- `Users` và `Boards` có quan hệ nhiều-nhiều qua `Board_Users`.
- `Users` và `Cards` có quan hệ nhiều-nhiều qua `Card_Assignees`.
- `Cards` và `Labels` có quan hệ nhiều-nhiều qua `Card_Labels`.
- `Comments` được liên kết với `Users` và `Cards` để lưu trữ các bình luận trong từng thẻ.
- `Activity_Log` lưu lại hoạt động của người dùng trên các `Boards` và `Cards`.

