# nbaski

Gray Scales

import cv2

teams = ['lakers', 'warriors', 'spurs']
for team in teams:
    img = cv2.imread(f'logos/{team}.png')
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    cv2.imwrite(f'logos/{team}_gray.png', gray)


Cropped images

def auto_crop(image_path, output_path):
    import cv2
    import numpy as np
    img = cv2.imread(image_path, 0)
    _, thresh = cv2.threshold(img, 1, 255, cv2.THRESH_BINARY)
    contours, _ = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    x, y, w, h = cv2.boundingRect(contours[0])
    cropped = img[y:y+h, x:x+w]
    cv2.imwrite(output_path, cropped)

teams = ['lakers', 'warriors', 'spurs']
for team in teams:
    auto_crop(f'logos/{team}_gray.png', f'logos/{team}_cropped.png')
