# Sun-animation
import pygame as kreggscode
import math
import sys

kreggscode.init()

window_size = (400, 400)
screen = kreggscode.display.set_mode(window_size)
kreggscode.display.set_caption("Sun Animation")
background_color = (255, 255, 204)
sun_color = (255, 204, 0)
triangle_color = (255, 153, 51)

clock = kreggscode.time.Clock()

def draw_rotated_sun(x, y, size, num_triangles, angle):
    kreggscode.draw.circle(screen, sun_color, (x, y), size)

    for i in range(num_triangles):
        angle_rad = 2 * math.pi * i / num_triangles + angle
        end_x = x + size * 2 * math.cos(angle_rad)
        end_y = y + size * 2 * math.sin(angle_rad)
        kreggscode.draw.polygon(screen, triangle_color,
         [(x, y), (end_x, end_y), 
        (x + size * math.cos(angle_rad + math.pi/num_triangles),
          y + size * math.sin(angle_rad + math.pi/num_triangles))])

running = True
sun_size = 80
num_triangles = 12
angle = 0

while running:
    for event in kreggscode.event.get():
        if event.type == kreggscode.QUIT:
            running = False

    screen.fill(background_color)

    x = window_size[0] // 2
    y = window_size[1] // 2

    angle += 0.01

    draw_rotated_sun(x, y, sun_size,
                 num_triangles, angle)

    kreggscode.display.flip()
    clock.tick(30)

kreggscode.quit()
sys.exit()
