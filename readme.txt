# for windows
python convert_guide.py -s $root
python train.py -s $root --iterations 60000 
SIBR_viewers\install\bin\SIBR_gaussianViewer_app_rwdi.exe -m <path to trained model> --rendering-size 2560 1920

#for middle scene
python train.py -s $root --iterations 70000 -m $output_root --position_lr_init 0.000064 --position_lr_final 0.0000032 --scaling_lr 0.004  --position_lr_max_steps 70000       
#for large scene
python train.py -s $root --iterations 90000 -m $output_root --position_lr_init 0.000032 --position_lr_final 0.00000032 --scaling_lr 0.002  --position_lr_max_steps 90000       
# final 
jw_high_120
cs_low_60
sk_all

# good rendering
zt_high2

#okish
by_low