# BT4-HQTCSDL  
# Tạo DataBase TKB gồm các Tables:
- GiangVien
- LichDay
- lop
- MonHoc
- Phong
## Tables GiangVien  
![{237748F3-E47C-453D-AD22-9A08475C71D5}](https://github.com/user-attachments/assets/77a894e3-a126-4b45-9381-fffc9d442399)  
Demo của bảng GiangVien  
![{7FFD4C58-9CFB-4E98-9F57-57723EF96C3C}](https://github.com/user-attachments/assets/a9ff870e-bba4-4e66-add8-7bc0fbac96e3)  
## Tables LichDay
![{8F659C44-6E55-446D-AEE5-17098F08B7C1}](https://github.com/user-attachments/assets/5905661c-3887-49fa-8f2c-c64b614086ab)  
Demo của bảng Lichday  
![{F6F62E84-6AE2-4C7B-974A-5B293D156B2B}](https://github.com/user-attachments/assets/11a13f53-bd9a-41d9-b522-13e94863476b)  
## Tables lop  
![{19D6D261-2D19-46FB-95E6-DA5CA10AE586}](https://github.com/user-attachments/assets/b688789f-9b82-4d24-a7d2-a96ce6257a5f)  
Demo của bảng lop  
![{2A9F8FB2-E636-4A7F-A99B-9B6E90674052}](https://github.com/user-attachments/assets/8078c55f-4d84-4ed3-9fa8-339a071977e2)  
## Tables MonHoc  
![{034CD765-D64A-4EBA-A08F-C56470D75D2F}](https://github.com/user-attachments/assets/c7409331-c3b8-4a34-8466-baff0ad95c2f)  
Demo của bảng MonHoc  
![{B66B1639-4A7F-439F-9E08-61767F4207D0}](https://github.com/user-attachments/assets/3f9cdaca-cddf-4572-8a59-b5d47f005d80)  
## Tables Phong  
![{7E120E02-5BFC-478A-801C-BC2AC5FE677A}](https://github.com/user-attachments/assets/707a79f2-ee4a-44c0-906a-006afebfcddf)  
Demo của bảng Phong  
![{8C5973FD-5043-4C18-B913-6B3A47C3F3CA}](https://github.com/user-attachments/assets/a041c4b8-1458-42b1-915d-18c373a0aeec)  
# Tạo bảng query để truy xuất thông tin dữ liệu đã nhập:  
 Sau khi đã tạo đủ các bảng chuẩn 3nf ta đã có thể tạo query để truy vẫn thông tin mong muốn
![{E6F497EC-375E-4112-8A45-5FBBD6038CE4}](https://github.com/user-attachments/assets/494e8c37-f4fb-4f7d-a67d-ffb52f52e29f)  
```
-- Khai báo khoảng thời gian cần kiểm tra lịch giảng dạy
use TKB
go
DECLARE @datetime1 DATETIME = '2025-04-16 06:30:00';
DECLARE @datetime2  DATETIME = '2025-04-16 09:10:00';

-- Truy vấn giảng viên bận giảng dạy trong khoảng thời gian trên
SELECT DISTINCT
    GV.Ten_GV        AS N'Họ tên GV',
    MH.Id_Monhoc       AS N'Môn dạy',
    l.Id_lop             AS N'Lớp học',
    ld.Id_phong       AS N'Phòng học',
    ld.Tietbatdau     AS N'tiết bắt đầu',
    ld.Tietkietthuc    AS N'tiết kết thúc'
FROM dbo.LichDay ld
JOIN dbo.GiangVien GV  ON ld.Id_GV = GV.Id_GV
JOIN dbo.MonHoc MH  ON ld.Id_Monhoc = MH.Id_Monhoc
JOIN dbo.lop  l ON ld.Id_lop = l.Id_lop 
WHERE
    CAST(ld.Ngay AS DATETIME) + CAST(ld.Tietkietthuc AS DATETIME) > @datetime1
AND CAST(ld.Ngay AS DATETIME) + CAST(ld.Tietbatdau AS DATETIME) < @datetime2;
