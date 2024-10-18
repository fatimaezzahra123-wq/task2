from PIL import Image
import numpy as np

def encrypt_image(image_path, output_path, key):
    img = Image.open(image_path)
    img_array = np.array(img)
    encrypted_array = img_array + key
    encrypted_array = np.clip(encrypted_array, 0, 255)
    encrypted_image = Image.fromarray(encrypted_array.astype('uint8'))
    encrypted_image.save(output_path)
    print(f"Encrypted image saved as: {output_path}")



def decrypt_image(image_path, output_path, key):

    img = Image.open(image_path)
    img_array = np.array(img)
    decrypted_array = img_array - key
    decrypted_array = np.clip(decrypted_array, 0, 255)  # Ensure pixel values remain valid
    decrypted_image = Image.fromarray(decrypted_array.astype('uint8'))

    decrypted_image.save(output_path)
    print(f"Decrypted image saved as: {output_path}")

def main():

    print("Welcome to the Image Encryption Tool!")
    operation = input("Do you want to encrypt or decrypt an image? (e/d): ").lower()
    image_path = input("Enter the path of the image: ")
    output_path = input("Enter the output path for the image: ")
    key = int(input("Enter a key (an integer for pixel manipulation): "))

    if operation == 'e':
        encrypt_image(image_path, output_path, key)
    elif operation == 'd':
        decrypt_image(image_path, output_path, key)
    else:
        print("Invalid operation. Please choose 'e' for encrypt or 'd' for decrypt.")

if __name__ == "__main__":
    main()
