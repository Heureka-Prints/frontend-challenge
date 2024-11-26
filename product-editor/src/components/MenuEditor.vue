<script setup lang="ts">
    import { reactive, computed } from "vue";
    import circleSvg from '@/assets/resources/shape-circle.svg';
    import heartSvg from '@/assets/resources/shape-heart.svg';
    import squareSvg from '@/assets/resources/shape-square.svg';
    import starSvg from '@/assets/resources/shape-star.svg';
    import triangleSvg from '@/assets/resources/shape-triangle.svg';

    const props = defineProps<{
        settings: {
            text: string;
            shape: string;
            aspectRatio: string;
            bgColor: string;
        };
        }>();
    interface AspectRatio {
        label: string;
        size: string; 
    }
    interface Shape {
        name: string; 
        svg: string;
    }
    const aspectRatios: AspectRatio[] = [ 
        { label: '20x30', size: '2x3' }, 
        { label: '30x40', size: '3x4' }, 
        { label: '50x70', size: '5x7' } 
    ];    
    
    const shapes: Shape[] = [
        { name: 'circle', svg: circleSvg },
        { name: 'heart', svg: heartSvg },
        { name: 'square', svg: squareSvg },
        { name: 'star', svg: starSvg },
        { name: 'triangle', svg: triangleSvg },
    ];
    // The menu contains an "Add to cart" button that's disabled until the text is changed.
    const initialText: string = props.settings.text;
    let textChanged = computed(() => props.settings.text !== initialText);
    const maxLength: number = 20; //Maximum text length allowed
    const isTooLong = computed(() => props.settings.text.length > maxLength);

    // Calculate remaining characters
    const remainingCharacters = computed(() => maxLength - props.settings.text.length);

    // Truncate text if it exceeds the limit
    if (props.settings.text.length > maxLength) {
    props.settings.text = props.settings.text.slice(0, maxLength);
    }

    // The 4 different customization drawers
    type Drawer = 'aspectRatio' | 'shape' | 'text' | 'bgColor';

    // interface for open drawers object
    interface OpenDrawers {
        aspectRatio: boolean;
        shape: boolean;
        text: boolean;
        bgColor: boolean;
    }

    const openDrawers = reactive<OpenDrawers>({
        aspectRatio: false,
        shape: false,
        text: false,
        bgColor: false,
    });

    // toggles the state of a specific drawer
    const toggleDrawer = (drawer: Drawer): void => {
        openDrawers[drawer] = !openDrawers[drawer];
    };


</script>

<template>
    <div class="menu-editor">
        <div class="menu-editor__heading">Customize your poster!</div>
        <!-- The menu contains the following inputs for customizing the product -->
        <div class="menu-editor__customizations">

            <!-- Aspect Ratio Selector -->
             <!-- Ratio: Aspect ratio of the product. Support at least 3 options, e.g. 2x3, 3x4, 5x7. -->
            <div class="customizations__dropdown customizations__dropdown--aspectratio">
                <div class="customization__title drawer-header" @click="toggleDrawer('aspectRatio')"> 
                    Ratio 
                    <span class="toggle-icon">{{ openDrawers.aspectRatio ? '-' : '+' }}</span>
                </div>
                <transition name="drawer">
                <div v-show="openDrawers.aspectRatio" class="customization__options drawer-content">
                    <div
                    v-for="ratio in aspectRatios"
                    :key="ratio.label"
                    :class="['customization__option',{ selected: settings.aspectRatio === ratio.size }]"
                    @click="settings.aspectRatio = ratio.size"
                    >{{ ratio.label }}
                    </div>
                </div>
                </transition>
            </div>

             <!-- Shape Selector -->
              <!-- Shape: Shape displayed at the top. There are some .svg files under resources/ which you can use. -->
             <div class="customizations__dropdown customizations__dropdown--shape">
                <div  class="customization__title drawer-header" @click="toggleDrawer('shape')">
                    Shape
                    <span class="toggle-icon">{{ openDrawers.shape ? '-' : '+' }}</span>
                </div>
                <transition name="drawer">
                <div v-show="openDrawers.shape" class="customization__options drawer-content">
                    <div
                    v-for="shape in shapes"
                    :key="shape.name"
                    :class="['customization__option', {selected: settings.shape === shape.name }]"
                    @click="settings.shape = shape.name"
                    >
                    <img :src="shape.svg" :alt="shape.name" class="shape-svg" />
                    <div>{{ shape.name }}</div>
                    </div>
                </div>
                </transition>
            </div>

            <!-- Text Input -->
             <!-- Text: Text displayed at the bottom. Validation is not necessary. -->
            <div class="customizations__dropdown customizations__dropdown--text">
                <div class="customization__title drawer-header" @click="toggleDrawer('text')">
                    Text
                <span class="toggle-icon">{{ openDrawers.text ? '-' : '+' }}</span>
                </div>
                <transition name="drawer">
                    <div v-show="openDrawers.text" class="drawer-content drawer-content--text">
                    <input
                        v-show="openDrawers.text"
                        v-model="settings.text"
                        type="text"
                        placeholder="Your poster text"
                        class="customization__text-input"/>
                        <p v-if="isTooLong" class="error-message">Text is too long. Maximum {{ maxLength }} characters allowed.</p>
                        <p v-else class="remaing-message">
                        Remaining characters: {{ remainingCharacters }}
                        </p>
                    </div>
                </transition>
            </div>

            <!-- Background Color for Fun :) -->
             <div class="customizations__dropdown customizations__dropdown--color">
                <div class="customization__title drawer-header" @click="toggleDrawer('bgColor')">
                    Background Color
                <span class="toggle-icon">{{ openDrawers.bgColor ? '-' : '+' }}</span>
                </div>
                <transition name="drawer">
                    <div v-show="openDrawers.bgColor" class="drawer-content">
                    <input
                        v-show="openDrawers.bgColor"
                        v-model="settings.bgColor"
                        type="color"
                        class="customization__bg-color"/>
                        <p v-if="isTooLong" class="error-message">Text is too long. Maximum {{ maxLength }} characters allowed.</p>
                        <p v-else>
                        Remaining characters: {{ remainingCharacters }}
                        </p>
                    </div>
                </transition>
            </div>
        </div>
         <!-- Add to Cart Button -->
        <!-- The menu contains an "Add to cart" button that's disabled until the text is changed. -->
         <div class="menu-editor__atc">
            <button :disabled="!textChanged" class="add-to-cart">
                Add to Cart
            </button>
         </div>
    </div>
</template>

<style scoped>
  @import '@/assets/stylesheets/component-editor.css';

</style>