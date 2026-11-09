# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |Xe con, sedan, SUV, taxi, xe bán tải |4 bánh |
| `truck` |Xe tải chở hàng, xe đầu kéo |6 bánh hoặc 8 bánh, có phần đầu kéo tách ra khỏi thùng hàng |
| `bus` |Xe buýt, minibus chở khách |4 bánh hoặc 6 bánh, dài, có đèn báo hoặc số hiệu của mỗi xe |
| `van` |Van, mini van chở hàng hoặc người |4 bánh nhưng phần đầu và thân xe gắn liền  |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: mỗi xe có 1 box riêng
- Vật thể bị che khuất: chỉ bao phần nhìn thấy nếu vẫn nhận diện được lớp    
- Vật thể bị cắt bởi rìa ảnh: box chỉ dừng ở rìa ảnh không đoán phần ngoài ảnh
- Vật thể rất nhỏ/mơ hồ: ghi rõ trường hợp và hỏi labcoach

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_002.jpg` |nhiều xe trồng lên nhau|vẽ box riêng cho từng xe còn nhận diện được |schema yêu cầu mỗi xe 1 box, xe bị che vẫn được gán nếu nhận diện được lớp |
| `drive_011.jpg` |xe đỏ bên góc phải trên bị cắt 1 phần đầu nhưng vẫn nhận ra là xe con |chọn " car "  |xe bị cắt vẫn gán nếu nhận diện được lớp, không đoán phần ngoài ảnh |
| `drive_017.jpg` |xe bị mờ khó phân biệt |chưa chốt ghi lại để hỏi |schema yêu cầu phân lớp theo loại xe, hình ảnh không đủ rõ thì không tự đoán |
| `drive_019.jpg` |hai xe che nhau |vẽ 2 box riêng quanh 2 phần nhìn thấy |schema quy định mỗi xe 1 box, không dùng 1 box cho 2 vật thể |
