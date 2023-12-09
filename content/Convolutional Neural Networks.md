Using a fully connected network for a image will be need a large sized memory & computational power since images have a width$\times$height = n amount of pixels(eg. $200 \times 200=40000$ pixels, with rgb multiply 3 more) Then we have the weight array size $n\times len(h)$ where $len(h)$ usually is not smaller than n($40000^2$ sized array)

For image processing we care about local neighborhoods