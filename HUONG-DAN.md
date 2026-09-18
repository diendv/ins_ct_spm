# Hướng dẫn phát hành app iOS qua GitHub (repo ins_ct_spm)

## Cấu trúc

```
ins_ct_spm/
├── index.html            # Trang cài đặt (nút bấm)
├── SpeedMaint.plist      # Manifest, trỏ tới file .ipa trong Releases
└── Release "app"         # Nơi chứa file nặng SpeedMaint.ipa
```

- **File .ipa** nằm trong **Releases** (tag cố định `app`) → repo không bị phình dung lượng.
- **plist** trỏ tới link cố định:
  `https://github.com/diendv/ins_ct_spm/releases/download/app/SpeedMaint.ipa`
- Vì tên tag (`app`) và tên file (`SpeedMaint.ipa`) **cố định** → **KHÔNG bao giờ phải sửa plist**.

## Link cài đặt (gửi cho người dùng)

Mở bằng Safari trên iPhone/iPad:
```
https://diendv.github.io/ins_ct_spm/
```

## Quy trình cập nhật bản mới (2 bước, làm trên web)

1. Vào repo → **Releases** → mở release **app** → bấm sửa (biểu tượng bút chì).
2. **Xoá** file `SpeedMaint.ipa` cũ → **kéo file build mới** (từ máy) vào, đặt **đúng tên** `SpeedMaint.ipa` → **Update release**.

> Xong. Không đụng vào plist. Link cài không đổi. Người dùng bấm cài là ra bản mới.
> (Phải xoá trước rồi mới upload vì GitHub không cho 2 file trùng tên trong 1 release.)

## Rollback về bản cũ (2 bước, y hệt)

1. Vào release **app** → **Xoá** `SpeedMaint.ipa` (bản lỗi).
2. **Kéo bản cũ tốt** (từ máy) vào, đặt tên `SpeedMaint.ipa` → **Update release**.

## Lưu ý quan trọng

- ⚠️ **Luôn giữ lại file build cũ trên máy** (đặt tên rõ như `SpeedMaint_1.0.13.ipa`, `SpeedMaint_1.0.14.ipa`...) để lỡ cần rollback thì upload lại.
- iOS tự đọc số phiên bản thật từ bên trong file .ipa, nên metadata trong plist không cần khớp tuyệt đối.
- Máy iPhone đã cài bản mới hơn: iOS không cho cài đè bản thấp hơn → phải xoá app rồi cài lại nếu muốn hạ version.
- Repo phải để **Public** thì GitHub Pages mới chạy.

## Vì sao dùng cách này

- Bản cũ (store.ekgis.vn) dùng TLS đời cũ (cipher CBC) → iOS 27 từ chối tải.
- GitHub (Pages + Releases) dùng **TLS 1.3 + AES-GCM** → iOS 27 tải được.
