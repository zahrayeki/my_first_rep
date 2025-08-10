import qrcode

def generate_qr(data, filename="qrcode.png"):
    # QR Code settings
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_H,
        box_size=10,
        border=4,
    )
    qr.add_data(data)
    qr.make(fit=True)

    # Create and save the image
    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filename)
    print(f"QR Code generated and saved as {filename}")

if __name__ == "__main__":
    text = input("Enter the text or URL to generate QR Code: ")
    generate_qr(text)
