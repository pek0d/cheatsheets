# to enable emoji font on arch distro

1.  `nano /etc/fonts/local.conf`
2.  paste text below

    "<?xml version="1.0"?>
     <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
     <fontconfig>

          <alias>
         	<family>sans-serif</family>
         	<prefer>
         	  <family>Sans</family>
         	  <family>Noto Color Emoji</family>
         	</prefer>
          </alias>

          <alias>
         	<family>serif</family>
         	<prefer>
         	  <family>Serif</family>
         	  <family>Noto Color Emoji</family>
         	</prefer>
          </alias>

          <alias>
           <family>monospace</family>
           <prefer>
         	 <family>Monospace</family>
         	 <family>Noto Color Emoji</family>
         	</prefer>
          </alias>

         </fontconfig>"

3.  `yay -S noto-fonts-emoji`
4.  fc-cache -v
5.  fc-cache -f
