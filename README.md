# watercolorfrom PIL import Image, ImageDraw, ImageFilter
import numpy as np

def generate_watercolor_image(width, height):
    """
    Generate an image with a simple watercolor-like gradient effect.
    """
    # Create an empty image
    image = Image.new('RGB', (width, height), color='white')
    draw = ImageDraw.Draw(image)
    
    # Create a gradient
    for y in range(height):
        r = int(255 * (y / height))
        g = int(255 * (1 - y / height))
        b = int(255 * 0.5)
        draw.line([(0, y), (width, y)], fill=(r, g, b))
    
    # Apply a blur filter to simulate watercolor blending
    image = image.filter(ImageFilter.GaussianBlur(radius=8))
    
    # Add some random noise for texture
    noise = np.random.normal(scale=20, size=(height, width, 3)).astype(np.uint8)
    noise_image = Image.fromarray(noise, 'RGB')
    image = Image.blend(image, noise_image, alpha=0.2)
    
    return image

def main():
    """
    Main function to create and save the watercolor image.
    """
    width, height = 800, 600
    image = generate_watercolor_image(width, height)
    image.save('watercolor_paint.png')
    image.show()

if __name__ == "__main__":
    main()
