Đầu tiên sau khi giải nén file zip ra, ta có thể thấy tên challange là unpackme2.exe (do file unpackme1 mình không chạy được nên mình sẽ chỉ viết wu cho bài này =(( )
Nếu tên nó đã vậy thì hẳn file pe này đã bị packed. Sử dụng DIE để phân tích tĩnh, ta thấy chương trình này đã đc pack lại bằng petite (cụ thể là 2.4 :)) )
![image](https://github.com/minhprovjp/CTFs/assets/78216350/add325f8-a2a8-4351-b58c-65b51addc82c)
Okay, xác định được packer, thử lên hỏi chị gồ xem có unpacker nào k. Hỏi chị gồ sơ qua 1 lượt thì ta có thể thấy mấy video yt guide trick set breakpoint ở mấy byte đầu của thanh ESP trong dump sau khi spam f7 vài lần ở ver 2.3 (khả năng cao trick này đã bị fix ver 2.4).
Mở IDA lên ta có thể thấy chương trình này đã bị pack hết r.
![image](https://github.com/minhprovjp/CTFs/assets/78216350/6e5044c2-5bc6-4a27-b25f-3775134e6afa)
Theo bản năng mình thử chạy file trong x64dbg, chạy chương trình lên và dump bằng scylla (và cũng không được luôn vì thử trick lỏ yt cho ver 2.3 r :)) ).
Mình nghĩ lại ok nếu đã bật th x64dbg lên r thì thử debug bằng nó luôn.
Nói qua chương trình này 1 chút, nếu các bạn run file lên các bạn dễ dàng có thể nhận thấy chương này rất đơn giản khi chỉ có 1 chức năng duy nhất là nhập input của chúng ta vào và báo về good và bad message.
Sau khi cửa sổ chương trình bật lên thì dĩ nhiên là chương này đã được unpack và cái chúng ta cần quan tâm chính là các string có trong chương trình.
Bật sang tab strings thì ngay dòng 1 đập vào mắt chúng ta chính là mục tiêu cần làm.
![image](https://github.com/minhprovjp/CTFs/assets/78216350/c072cbb0-63d6-4f8d-9ed1-1e17832ef8c0)
Đi đến dòng "Good boy", mình đoán lệnh input sẽ gần đó, vậy nên mình kéo lên ngó thử và đúng là chương trình có đoạn này thật. :))
![image](https://github.com/minhprovjp/CTFs/assets/78216350/5331b1c0-5b2d-458c-b57d-1284479f2c13)
Mình sẽ thử đặt breakpoint tại dòng pop esi và sau đó spam f7 f8 để xem chương trình sẽ xử lý chuỗi input của chúng ta thế nào. Ở đây mình sẽ nhập 123456789.
![image](https://github.com/minhprovjp/CTFs/assets/78216350/40653ec9-f5cb-44cc-b0fc-283bdf0b31f8)
Chương trình đã dừng sau khi mình input vào. Spam f8, chúng ta dễ dàng chạy qua các lệnh của chương trình cho đến lệnh call đầu tiên sau lệnh pop esi.
Thử f7 vào xem có gì hot, và nhân vật chính của chúng ta đã xuất hiện. Function check các ký tự input với các ký tự có trong flag.
![image](https://github.com/minhprovjp/CTFs/assets/78216350/ac184901-5906-463a-a845-d6988cec5bfe)
Sau khi ghép các ký tự của flag, ta thu được flag của challange: yeu_chim_se_UJg7Udn
Kết quả: 
![image](https://github.com/minhprovjp/CTFs/assets/78216350/b39dc525-8182-416f-b49a-d4a5936747a5)


