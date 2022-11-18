import os
from os import system, listdir, path, remove, getenv; from os.path import isfile, islink, isdir
from win32api import GetLogicalDriveStrings
from tempfile import gettempdir
import time
import urllib.request
from subprocess import run
from shutil import rmtree

drive_letter = getenv('HOMEDRIVE')

def delete(path):
        if isfile(path) or islink(path):
            remove(path)
        elif isdir(path):
            rmtree(path)


def battery():
    battery_saver = input("Would you like to enable the battery saver? (y/n) ")
    if battery_saver == "y":
        os.system('cmd /k "powercfg /setdcvalueindex scheme_current sub_energysaver esbattthreshold 100"')
        power()
    else:
        power()

def drivers():
    print("Would you like to manually update your NVIDIA GPU driver? (y/n) ")
    driver = input("ONLY FOR NVIDIA USERS! ENTER 'n' IF NOT: ")
    if driver == "y":
        urllib.request.urlretrieve("https://github.com/Aetopia/NVIDIA-Driver-Downloader/releases/download/v1.3.4.3/nvddl.exe", "nvddl.exe")
        run(['nvddl.exe', '-dl', '-s'], cwd=gettempdir())
        print("Have fun with your battery saving PC!")
        time.sleep(3)
        exit()

def defrag():
    defrager = input("Would you like to defrag your drives? (y/n) ")
    if defrager == "y":
            drives = GetLogicalDriveStrings().split("\000")
            for drive in drives:
                if path.exists(drive):
                    system(f"defrag.exe {drive}")
                    drivers()
    drivers()

def clean():
    clean_files = input("Would you like to clean junk files? (y/n) ")
    if clean_files == "y":
        junk = listdir(gettempdir())
        for temp in junk:
            try:
                delete(f"{gettempdir()}\\{temp}")
                junk2 = listdir(f"{drive_letter}\\Windows\\Temp")
                for temp2 in junk2:
                    delete(f"{drive_letter}\\Windows\\Temp\\{temp2}")
            except:
                defrag()
    else:
        defrag()

def hibernation():
    hibernation_enable = input("Would you like to enable hibernation? (y/n) ")
    if hibernation_enable == "y":
        os.system('cmd /k "powercfg /hibnernate on"')
        clean()
    else:
        clean()

def background():
    background_apps = input("Would you like to disable background apps? (y/n) ")
    if background_apps  == "y":
        os.system('cmd /k "Reg Add HKCU\Software\Microsoft\Windows\CurrentVersion\BackgroundAccessApplications /v GlobalUserDisabled /t REG_DWORD /d 1 /f"')
        hibernation()
    else:
        hibernation()

def brightness():
    brightness_screen = input("Would you like to reduce the brightness of your screen? (y/n) ")
    if brightness_screen == "y":
        os.system('cmd /k "powershell (Get-WmiObject -Namespace root/WMI -Class WmiMonitorBrightnessMethods).WmiSetBrightness(1,75)"')
        background()
    else:
        background()

def power():
    power = input('Would you like to enable the "Power Saver" power plan? (y/n) ')
    if power == "y":
        os.system('cmd /k "powercfg.exe /setactive a1841308-3541-4fab-bc81-f71556f20b4a"')
        brightness()
    else:
        brightness()


def main():
    print("███████╗███╗░░██╗███████╗██████╗░░██████╗░██╗░░░██╗░██████╗░█████╗░██╗░░░██╗███████╗██████╗░")
    print("██╔════╝████╗░██║██╔════╝██╔══██╗██╔════╝░╚██╗░██╔╝██╔════╝██╔══██╗██║░░░██║██╔════╝██╔══██╗")
    print("█████╗░░██╔██╗██║█████╗░░██████╔╝██║░░██╗░░╚████╔╝░╚█████╗░███████║╚██╗░██╔╝█████╗░░██████╔╝")
    print("██╔══╝░░██║╚████║██╔══╝░░██╔══██╗██║░░╚██╗░░╚██╔╝░░░╚═══██╗██╔══██║░╚████╔╝░██╔══╝░░██╔══██╗")
    print("███████╗██║░╚███║███████╗██║░░██║╚██████╔╝░░░██║░░░██████╔╝██║░░██║░░╚██╔╝░░███████╗██║░░██║")
    print("============================================================================================")
    power()
main()
