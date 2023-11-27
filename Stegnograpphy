import cv2
import os

def text_to_binary(text):
    binary_message = ''.join(format(ord(char), '08b') for char in text)
    return binary_message

def binary_to_text(binary_message):
    text = ''.join(chr(int(binary_message[i:i+8], 2)) for i in range(0, len(binary_message), 8))
    return text

def encrypt_image(image_path, secret_message, password):
    img = cv2.imread(image_path)

    binary_message = text_to_binary(secret_message)
    binary_message += '1111111111111110'  # Add a delimiter to mark the end of the message

    n, m, z = 0, 0, 0
    for bit in binary_message:
        img[n, m, z] = (img[n, m, z] & ~1) | int(bit)
        n, m, z = n + 1, m + 1, (z + 1) % 3

    cv2.imwrite("Encryptedmsg.png", img)

    print("Message encrypted successfully.")
    os.system("start Encryptedmsg.png")

def decrypt_image(encrypted_image_path, password):
    img = cv2.imread(encrypted_image_path)

    n, m, z = 0, 0, 0
    binary_message = ""

    entered_password = input("Enter passcode for decryption: ")

    if password == entered_password:
        while True:
            bit = img[n, m, z] & 1
            binary_message += str(bit)
            n, m, z = n + 1, m + 1, (z + 1) % 3

            # Check for the delimiter to mark the end of the message
            if binary_message[-16:] == '1111111111111110':
                break

        binary_message = binary_message[:-16]  # Remove the delimiter
        decrypted_message = binary_to_text(binary_message)

        print("Decryption message:", decrypted_message)
    else:
        print("Not a valid passcode.")


original_image_path = 'mypic.jpg'
secret_message = input("Enter secret message: ")
password = input("Enter password: ")

encrypt_image(original_image_path, secret_message, password)
decrypt_image('Encryptedmsg.png', password)
