import qrcode

def generate_qr(data, filename="qrcode.png"):
    # تنظیمات QR Code
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_H,
        box_size=10,
        border=4,
    )
    qr.add_data(data)
    qr.make(fit=True)

    # ساخت تصویر
    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filename)
    print(f"✅ QR Code ساخته شد و در فایل {filename} ذخیره شد.")

if __name__ == "__main__":
    text = input("متنی که میخوای QR Code بشه رو وارد کن: ")
    generate_qr(text)
