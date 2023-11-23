# The V-HACD library decomposes a 3D surface into a set of "near" convex parts.
Original readme [see here](https://github.com/RoboticManipulation/v-hacd/tree/master).

# Example
![Convex-hull vs. ACD](doc/chvsacd.png)

# Installing the Package

On Windows, go to the ./app directory and run 'cmake -DCMAKE_GENERATOR_PLATFORM=x64 CMakeLists.txt' and then load the solution file

On Linux, use this:
```bash
cd app
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

# Usage
```bash
cd build
decompose mesh.obj -out_path ./ -out_file decomp -e 0.01 -d 15 -r 10000000 -r 128
```

# Documentation
Click this link to find detailed documentation for how to use the library:
- [pdf](doc/presentation/v-hacd_v4.pdf)
- [pptx](doc/presentation/v-hacd_v4.pptx)
- [Google presentation](https://docs.google.com/presentation/d/1OZ4mtZYrGEC8qffqb8F7Le2xzufiqvaPpRbLHKKgTIM/edit?usp=sharing)

# Tuning parameters

The default values are currently designed to give a fast and basic approximation of a shape.

If you want as accurate results as possible and don't care if it takes quite a bit longer you can use a small error threshold (-e 0.01) and a high voxel resolution of ten million (-r 10000000) and a relatively high number of convex hulls say 128 (-h 128).

Finally you can set the maximum decomposition depth to much higher than the default value of 10. Setting it to say 15 (-d 15) will allow the algorithm to recurse much more deeply into the shape. A higher depth value requires a 64 bit build of the library.

Example: TestVHACD beshon.obj -e 0.01 -d 15 -r 10000000 -r 128

Usually this may be overkill for your use case but if you have say machined parts with sharp angles, these settings have a better chance of giving a good result.

Note that setting the maximum decomposition depth to 15 will make the tool run a very long time (possibly multiple minutes) but it will likely give the most precise results.

The default value for decomposition depth is currently ten and it goes in powers of two. So the default value considers a maximum of 1,024 hulls but with a depth of 15 it will consider 32,768 convex hull fragments.