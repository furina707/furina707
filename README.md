@echo off
chcp 65001 >nul
title 文件查看器

echo ========================================
echo     完整文件列表（含隐藏内容）
echo ========================================
echo.
echo 当前位置: %cd%
echo.

echo [树形结构]
tree /F /A
echo.

echo [隐藏文件夹内容 - .git]
if exist ".git" (
    echo.
    echo === .git 主要文件 ===
    dir /b ".git" | findstr /v "objects"
    echo.
    echo === .git 分支信息 ===
    if exist ".git\refs\heads" dir /b ".git\refs\heads"
)

echo.
echo [所有文件（含隐藏）]
dir /b /a
echo.

echo [统计]
for /f %%a in ('dir /b /a-d 2^>nul ^| find /c /v ""') do echo 普通文件: %%a 个
for /f %%a in ('dir /b /ad 2^>nul ^| find /c /v ""') do echo 普通文件夹: %%a 个
for /f %%a in ('dir /b /ah 2^>nul ^| find /c /v ""') do echo 隐藏项目: %%a 个

pause
