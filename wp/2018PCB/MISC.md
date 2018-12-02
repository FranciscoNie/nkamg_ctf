## MISC Write Up

### Traffic Light

1. 使用 `ImageMagic` 或 `PhotoShop` 等工具逐帧分离 `gif` 文件形成 `png`：

   ```cmd
   $ magick convert Traffic_Light.gif -coalesce png/%05.png
   ```

   *PostScript*：安装 ImageMagic

   ```cmd
   $ choco install ImageMagic
   ```

2. 使用以下 bash 命令：

   ```bash
   $ cd png
   
   $ ll | awk '{print $5}' | tr -d '\n' | sed 's/5333/1/g; s/5042//g; s/5282/0/g; s/5347/\n/g;' > encoding.txt
   ```

3. 创建以下 `python` 脚本并运行，即得到 flag：

   ```python
   with open("encoding.txt","r") as f:
   	l = f.read().splitlines() 
   
   int_l = [int(l[i+1],2) for i in range(len(l)-1)]
   char_l = [chr(int_l[i]) for i in range(len(int_l))]
   
   print(''.join(char_l))
   ```

   ```bash
   $ python decode.py
   flag{Pl34s3_p4y_4tt3nt10n_t0_tr4ff1c_s4f3ty_wh3n_y0u_4r3_0uts1d3}
   ```

### Quotes

1. 使用以下 bash 命令：

   ```bash
   $ sed 's/+//g' Quotes.txt | awk -v RS=" " '{print length($1)}' > number.txt
   ```

2. 创建以下 `python` 脚本并运行：

   ```python
   with open("number.txt", "r") as f:
   	l = f.read().splitlines()
   
   
   l_i = [int(i,10) for i in l]
   l_c = [chr(ord('a') + i -1) if i is not 0 else ' ' for i in l_i]
   
   print(''.join(l_c))
   ```

   ```bash
   $ python decode.py
   word games
   ```

