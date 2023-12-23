Data  link
https://drive.google.com/drive/folders/15TKaHRj5V01WEkkQeVzX-XvMZ4qCU3_f?usp=sharing

Extract sk_all.zip and put in ./data folder

Procedure
Data Processing
mkdir eq_images
ffmpeg -i input.mp4 -r 1 eq_images/eq_image%04d.png
mkdir pers_images
python Perspective-and-Equirectangular\equir2pers.py --input eq_images --output pers_images
python3 instant-ngp\scripts\colmap2nerf.py --images pers_images --run_colmap

ffmpeg -i BYlow.mp4 -ss 20 -t 60 -c:v libx264 -c:a aac -strict experimental BYlow_trim.mp4

Training
# for windows
python convert_guide.py -s $root
python train.py -s $root --iterations 60000 
SIBR_viewers\install\bin\SIBR_gaussianViewer_app_rwdi.exe -m <path to trained model> --rendering-size 2560 1920

#for middle scene
python train.py -s $root --iterations 70000 -m $output_root --position_lr_init 0.000064 --position_lr_final 0.0000032 --scaling_lr 0.004  --position_lr_max_steps 70000       
#for large scene
python train.py -s $root --iterations 90000 -m $output_root --position_lr_init 0.000032 --position_lr_final 0.00000032 --scaling_lr 0.002  --position_lr_max_steps 90000   