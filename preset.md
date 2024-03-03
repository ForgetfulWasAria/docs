# How to Modify a Preset
Presets configure Fooocus to create a certain kind of image output. This file should help you modify an existing preset to be more to your liking. I wanted a preset that loaded dreamshaperXL"s turbo model without me having to make the changes by hand every time I start Fooocus.

You'll need a working copy of Fooocus and a text editor. You can use any editor you like but one that can do syntax highlighting on json files, like Notepad++ or VS Code, is helpful to avoid errors.

Let me know if any of this is wrong, unclear, or if there"s something to add. I am not an expert.

## Modifying a Preset
### Make a Copy of an Existing Preset
This is the easiest way to get started. You shouldn't modify the presets that come with Fooocus because they will be reset whenever Fooocus updates. 
</br> If you installed by using git clone, presets go in the `Fooocus\presets` directory. If you used the easy installer your Fooocus directory will look something like this:
```
- Fooocus
        - run.bat
        - run_realistic.bat
        - run_anime.bat
        - Fooocus
                - presets
                        - anime.json
                        - default.json
                        - realistic.json
                        - maybe others
                - modules
                - lots of other directories and file
```
Presets will be in the `Fooocus\Fooocus\presets` directory.

You can use your File Manager (at least on Windows) to copy one of them by holding the Ctrl key and dragging a preset to an empty space in the same directory. You could also do it from a command line. I"ll assume you know how to do that if you want to.

### Rename the Preset
Give your preset whatever name you"d like to so that you"ll remember what it does. I chose "turbo_local" so I"d know it was a turbo preset and that I had made it. Press F2 white the file is selected to rename it. Make sure it still has the .json extension.

### Make Changes
Open your new preset in your text editor. Below is a list of settings found in the /Fooocus/modules/config.py file. Many of these will already be in the preset file and changing their value is the easiest way to make a new preset. Others will have to be added if you need them.
</br>I am not an expert on JSON, this is only how I modified the presets to make my own.
#### Editors
While you can use any editor you like, I'm going to use Visual Studio Code as it is free and has a few convenient features when working with JSON files:
* It colorizes brackets, meaning that the opening and closing brackets are given the same color, making it easy to see which brackets go with which.
* It has syntax highlighting, meaning that each piece of text has a color according to what type it is (that is what function is has).

In general if you edit something it should end up the same color it was when you started.
#### A Note on Brackets
There are three types of brackets, only two of which I've seen in the presets. These have different meanings and you shouldn't change one with the other.
* Parenthesis, or curved brackets are not in any of the preset files. They look like this: `()`
* Square brackets look like this: `[]` On a US English keyboard, they are the near the Enter/Return key, above the quotes.
* Curly brackets look like this: `{}` and are on the same key as the square brackets.

Brackets on the same line and of the same type should also be the same color. Brackets are always in pairs and deleting one of them will cause error messages.
#### Structure of the Preset File
The preset looks a bit like this
```
{
    item,
    another item,
    yet another item,
    the last item
}
```
Note the pair of curly brackets and that the last item in the file doesn't have a comma at the end.
</br>Each item follows a pattern like this:
```
"setting" : value
```
where setting is one of the settings from the list below. After each setting name, I've listed the type of value that the setting takes. There are three types:
* Numbers are either whole numbers (1, 2, 10) or decimals (7.2, 0.8, 1.64). Decimals less than one should have a leading zero, so 0.4 not .4.
* Strings can be anything but they must be enclosed in quotes:
```
"myString value"
```
* Booleans are either true or false. True turns the setting on, false disables it. Always use all lower case: true not True.
* Arrays are one or more values enclosed in square brackets:
```
"setting" : 
    [
        first_item,
        another,
        last_item
    ]
```
In general, change the items, but don't change the brackets. Note that the last item doesn't have a comma after it. Arrays can have Numbers, Strings, or other Arrays in them. As long as you leave the brackets alone (unless you're deleting an entire item) you should be ok.

It's a good habit to make a change and then test it by starting Fooocus and seeing if it works or if there are error messages on the console.

## Using your Preset

### Original Fooocus
Restarting Fooocus should cause your preset to show up with the rest of the presets. If you can"t see it, check Troubleshooting below. 

### To Start with your Preset
Run Fooocus the way you normally would, using `--preset your_preset_name`

### Original Fooocus with the Easy Installer
In the top level directory above, there are several batch files. Copy one of them (Ctrl + Drag to an empty space) and rename it (F2) to something you"ll recognize. Since my preset is "turbo_local.json" I chose "run_turbo_local.bat" Make sure that you don"t change the file extension. Use this new .bat file when you want to use your preset.

### Testing
Start up Fooocus and make sure that the model and any loras have been loaded. Many of the settings below will only show up in the Developer Debug Mode on the Advanced page. Generate some images and see if they are generated the way you think they should be. Finally, check the console. If you don"t see any errors, enjoy your new preset.

## List of Settings
Fooocus explains what most of these do in the interface. This section gives an example of how they look in a preset file. The examples are taken from the turbo preset I modified and will be different from the values you see.
### Fooocus (lllyasviel)
#### default_model (String)
This is the name of the checkpoint you want your preset to load surounded by double quotes. Be sure to include the .safetensors extension.
```
"default_model": "dreamshaperXL_v2TurboDpmppSDE.safetensors",
```
#### previous_default_models
????
#### default_refiner (String)
The name of the refiner your preset should load. This works like the default model.
```
"default_refiner": "None",
```
#### default_refiner_switch (Number)
How far through Fooocus should switch to your refiner, if one is present. This will be a number between 0 and 1. 0.5-0.8 is a common range.
```
"default_refiner_switch": 0.5,
```
#### default_loras (Special)
A list of five lora slots. Change "None" to the name of the lora, including extension, and set the strength as a number. The default looks like this:
```
"default_loras": [
        [
            "None",
            1.0
        ],
        [
            "None",
            1.0
        ],
        [
            "None",
            1.0
        ],
        [
            "None",
            1.0
        ],
        [
            "None",
            1.0
        ]
    ],
```
Notice the square bracket by "default lora": and the one at the bottom on a line by itself with a comma. Those are paired. If your editor colors brackets, they should be the same color.
Inside are five slots for loras, each surrounded by square brackets ending with a comma, except the last one that doesn"t have a comma. Each looks like this:
```
        [
            "None",
            1.0
        ],
```
To load a lora, just change the None to the lora"s file name including the safetensors extension. You can change the strength right below by changing 1.0 to 0.8 or 1.5 or any other value you desire.
#### default_config_scale (Number)
Sets how closely to follow the prompt, with high values allowing the model more freedom.
```
"default_cfg_scale": 2.0,
```
#### default_sample_sharpness (Number)
Controls how sharp the resulting image is.
```
"default_sample_sharpness": 3.0,
```
#### default_sampler (String)
Sets the sampler to use for image generation.
```
"default_sampler": "dpmpp_sde",
```
#### default_scheduler (String)
Sets the noise scheduler.
```
"default_scheduler": "karras",
```
#### default_styles (Array)
Selects which of Fooocus"s styles should be enabled when this preset is loaded. Each item in the Array is a String.
```
"default_styles": [
        "Fooocus V2",
        "Fooocus Enhance",
        "Fooocus Sharp"
    ],
```
#### default_prompt (String)
Sets a prompt at start up.
```
"default_prompt": "",
```
#### default_prompt_negative (String)
Sets the text in the negative prompt at start up.
```
"default_prompt_negative": "",
```
#### available_aspect_ratios (Array)
Sets the list of aspect ratios (resolutions) that will appear in the Fooocus UI. Note that using resolutions SDXL wasn't trained on will lower quality. Unless you know another working resolution, I wouldn"t change this.
```
"available_aspect_ratios": [
        "704*1408", "704*1344", "768*1344", "768*1280", "832*1216", "832*1152",
        "896*1152", "896*1088", "960*1088", "960*1024", "1024*1024", "1024*960",
        "1088*960", "1088*896", "1152*896", "1152*832", "1216*832", "1280*768",
        "1344*768", "1344*704", "1408*704", "1472*704", "1536*640", "1600*640",
        "1664*576", "1728*576"
    ],
```
#### default_aspect_ratio (String)
This selects the resolution for image generation. This should be one of the pairs listed in your Fooocus UI with the numbers separated by an asterisk. For example, to set the resolution to 896 pixels wide by 1152 tall, you"d use the following line:
```
"default_aspect_ratio": "896*1152",
```
#### default_performance (String)
Which performance preset to use of the ones listed in the UI.
```
"default_performance": "Speed",
```
#### default_advanced_checkbox (Boolean)
Whether to show the Advanced settings at start up or not.
```
"default_advanced_checkbox": true,
```
#### default_max_image_number (Number)
This sets how many images are queued when the Generate button is pressed. I tested and it seems you can set this to 1000 without a problem. I did not actually generate 1000 images though. In the past, I"ve used 100 without a problem.
```
"default_max_image_number": 32,
```
#### default_image_number (Number)
This sets where the slider is at start up. It should be less than or equal to the default_max_image_number.
```
"default_image_number": 4,
```
#### checkpoint_downloads, lora_downloads, embeddings_downloads (Special)
These work the same way, Fooocus will download the indicated checkpoint if it isn"t in your model directory. Usually you will want this to be the default_model you selected.
</br> **Note that this item is surrounded by curly brackets in all of the presets, not square brackets.** </br> The realistic preset has this:
```
"checkpoint_downloads": {
        "realisticStockPhoto_v20.safetensors": "https://huggingface.co/lllyasviel/fav_models/resolve/main/fav/realisticStockPhoto_v20.safetensors"
    },
```
If you do not want your preset to ever download a model you can do this:
```
"checkpoint_downloads": {},
    "embeddings_downloads": {},
    "lora_downloads": {},
```

#### default_inpaint_engine_version (Number)
This sets which inpaint model will be used. None of the presets I looked at used this.
```
"default_inpaint_engine_version": 2.6,
```
#### default_cfg_tsnr (Number)
???? I"m not sure what the difference between this and default_cfg_scale is.
```
"#### default_cfg_tsnr": 7.0,
```
#### default_overwrite_step (Number)
This changes the number of steps used in generating an image. It is particularly useful for Turbo models that need only 6-8 steps.
```
"default_overwrite_step": 20,
```
#### default_overwrite_switch (Number)
????
#### example_inpaint_prompts (Array)
This sets the list that appears below the inpainting section. You can add or change these prompts using this item:
```
"example_inpaint_prompts": [
        "highly detailed face",
        "detailed girl face",
        "detailed man face",
        "detailed hand",
        "beautiful eyes",
        "Whatever prompt you want"
    ],
```
Notice that the last item doesn't have a comma at the end.

#### default_output_format (String)
Controls the image format Fooocus will produce. Can be "jpg", "png", or "webp." If not set, Fooocus will produce PNG files.
```
"default_output_format": "jpg",
```
#### default_overwrite_upscale (Number)
???? I would think this controls the upscale factor but I'm not sure.

#### default_loras_min_weight (Number)
This is the lowest value you can set for the lora weight using the slider.
```
"default_loras_min_weight": -5,
```

#### default_loras_max_weight (Number)
This is the highest value you can set for the lora weight using the slider. If you set this to a value lower or the same as the default_loras_min_weight, you won't be able to change the lora weight with the slider.
```
"default_loras_max_weight": 5,
```

#### default_max_lora_number (Number)
This controls how many loras the interface will show. I tested values from 1 to 20 and the interface showed that many. Setting it to 0 will cause the interface to show the default 5.
```
"default_max_lora_number": 10,
```

#### default_save_metadata_to_images (Boolean)
Whether to include metadata in the images themselves. Fooocus will always produce the log.html files.
```
"default_save_metadata_to_images": false,
```

#### default_metadata_scheme (String)
This determines if metadata in files is in JSON format (fooocus) or the format Automatic1111 uses. If default_save_metadata_to_images is false or absent, this will have no effect.
```
"default_metadata_scheme": "fooocus",
```
or 
```
"default_metadata_scheme": "a1111",
```

#### metadata_created_by (String)
Allows you to put your name, handle or something else in the metadata. Again, this only matters if metadata is saved to images.
```
"metadata_created_by": "Your_Message_Here",
```

#### default_inpaint_mask_model (String)
#### default_inpaint_mask_sam_model (String)
These settings should only be changed if you have an alternative inpaint mask or sam model that you want Fooocus to use.
```
"default_inpaint_mask_sam_model": "model.safetensors",
```
#### default_inpaint_mask_cloth_category (String)
The model you specified above should have instructions on the correct category to use.
```
"default_inpaint_mask_cloth_category": "category",
```
#### default_black_out_nsfw (Boolean)
Controls whether Fooocus will black out images it detects as Not Safe for Work.
```
"default_black_out_nsfw": true,
```


Thank you for coming to my TED talk.
