# Build process

> @note For some reasons fontforge (Ligaturizer manual generation) can't generate the font

Log output

```sh
fontforge -lang py -script ligaturize.py "fonts/consolas-font-original/consola.ttf" \
    --output-dir="$CWD/fonts/output/" \
    --output-name='Consolas ligaturized v2'

# ...saving to '/fonts/output/LigaConsolas.ttf' (Liga Consolas)
# Save Failed
# Traceback (most recent call last):
#   File "ligaturize.py", line 340, in <module>
#     main()
#   File "ligaturize.py", line 337, in main
#     ligaturize_font(**vars(parse_args()))
#   File "ligaturize.py", line 296, in ligaturize_font
#     font.generate(output_font_file)
# EnvironmentError: Font generation failed
```

> So, instead we'll be using [Ligaturizer automatic generation](https://github.com/ToxicFrog/Ligaturizer#automatic)

```sh
## Pull submodules (Fira font, etc...)
git submodule update --init --recursive


## Copy Consolas original font to Ligaturized font folder
cp -r _build/consolas-font-original _build/Ligaturizer/fonts


## Edit build.py
prefixed_fonts = [
]
renamed_fonts = {
  'fonts/consolas-font-original/*.ttf': 'Consolas ligaturized v2'
}

## Run the build
cd _build/Ligaturizer && make

## Copy ligaturized consolas font to repo root
cp -r fonts/output/*.ttf ../../
```