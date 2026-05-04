# Transformasi 
Program: Transformasi Refleksi Dinamis
Deskripsi:
- Menampilkan objek (kotak) di Kuadran 1
- Menampilkan bayangan hasil refleksi di Kuadran 2
- Objek dapat digeser dengan mouse (drag)
- Bayangan mengikuti secara real-time
- Sumbu refleksi bersifat dinamis (berubah sesuai posisi objek)
"""

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.path import Path

# DATA AWAL OBJEK (KOTAK)
points = np.array([
    [2, 2],
    [4, 2],
    [4, 4],
    [2, 4]
])

# Variabel kontrol drag
dragging = False
start_mouse = None
start_points = None


# FUNGSI REFLEKSI DINAMIS
def reflect_dynamic(points):
    """
    Melakukan refleksi terhadap garis vertikal x = a
    dimana a berubah sesuai posisi objek
    """
    a = np.mean(points[:,0]) - 2.5  # sumbu dinamis

    reflected = points.copy()
    reflected[:,0] = 2*a - points[:,0]

    return reflected, a



# CEK KLIK DI DALAM OBJEK

def is_inside(x, y, polygon):
    return Path(polygon).contains_point((x, y))



# FUNGSI GAMBAR

def draw():
    plt.cla()

    # Gambar objek asli
    p = np.vstack([points, points[0]])
    plt.plot(p[:,0], p[:,1], marker='o', label="Asli (Q1)")

    # Gambar bayangan
    rp, axis = reflect_dynamic(points)
    rp = np.vstack([rp, rp[0]])
    plt.plot(rp[:,0], rp[:,1], marker='o', label="Cermin (Q2)")

    # Gambar sumbu refleksi
    plt.axvline(axis, linestyle='--', label="Sumbu Dinamis")

    # Garis sumbu koordinat
    plt.axhline(0)
    plt.axvline(0)

    plt.grid()
    plt.legend()
    plt.xlim(-10, 10)
    plt.ylim(-10, 10)
    plt.title("Transformasi Refleksi Dinamis (Drag dengan Mouse)")



# EVENT MOUSE

def on_click(event):
    global dragging, start_mouse, start_points

    if event.inaxes and is_inside(event.xdata, event.ydata, points):
        dragging = True
        start_mouse = np.array([event.xdata, event.ydata])
        start_points = points.copy()


def on_release(event):
    global dragging
    dragging = False


def on_motion(event):
    global points

    if dragging and event.inaxes:
        delta = np.array([event.xdata, event.ydata]) - start_mouse

        new_points = start_points + delta

        # Batasi agar tetap di Kuadran 1
        new_points[:,0] = np.maximum(new_points[:,0], 0.1)
        new_points[:,1] = np.maximum(new_points[:,1], 0.1)

        points[:] = new_points

        draw()
        plt.draw()



# MAIN PROGRAM

fig = plt.figure()
draw()

fig.canvas.mpl_connect('button_press_event', on_click)
fig.canvas.mpl_connect('button_release_event', on_release)
fig.canvas.mpl_connect('motion_notify_event', on_motion)

plt.show()