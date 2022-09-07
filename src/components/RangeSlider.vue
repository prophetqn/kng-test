<template>
    <div ref="sliderContainer" class="slider-container">
        <div ref="leftSpace" class="left-bar"></div>
        <div 
            ref="slider"
            @mousedown.prevent="startSlide" 
            class="slider shadow"
        >
            <i class="bi bi-chevron-left"></i>
            <span>$ {{ value.toLocaleString('en-US') }}</span>
            <i class="bi bi-chevron-right"></i>
        </div>
        <div class="right-bar"></div>
    </div>
</template>

<script>
export default {
    props: {
        range: {
            type: Number
        },
        interval: {
            type: Number
        },
    },
    data() {
        return {
            value: 0,
            distance: null,
            sliding: false,
            posXSlider: 0,
            posXMouse: null
        }
    },
    mounted() {
        this.setDistance();
        window.addEventListener('resize', this.setDistance);
        window.addEventListener('mousemove', this.doSlide);
        window.addEventListener('mouseup', this.stopSlide);
    },
    unmounted() {
        window.removeEventListener('resize', this.setDistance);
        window.removeEventListener('mousemove', this.doSlide);
        window.removeEventListener('mouseup', this.stopSlide);
    },
    methods: {
        setDistance() {
            let oldDistance = this.distance;
            this.distance = this.$refs['sliderContainer'].offsetWidth - this.$refs['slider'].offsetWidth;
            if (oldDistance > 0) {
                this.posXSlider = this.posXSlider / oldDistance * this.distance;
                this.$refs['leftSpace'].style.flexBasis = this.posXSlider + 'px';
            }
        },
        startSlide(e) {
            this.sliding = true;
            this.posXMouse = e.clientX;
            this.$refs['slider'].style.cursor = 'grabbing';
        },
        doSlide(e) {
            if (this.sliding) {
                let mouseMoveDistance = e.clientX - this.posXMouse;
                this.posXSlider += mouseMoveDistance;
                this.posXMouse = e.clientX;
                this.posXSlider = Math.max(this.posXSlider, 0);
                this.posXSlider = Math.min(this.posXSlider, this.distance);
                this.$refs['leftSpace'].style.flexBasis = this.posXSlider + 'px';
                this.passValue();
            }
        },
        stopSlide() {
            this.sliding = false;
            if (this.$refs['slider']) {
                this.$refs['slider'].style.cursor = 'grab';
            }
        },
        passValue() {
            this.value = Math.round((this.posXSlider / this.distance * this.range) / this.interval) * this.interval;
            this.$emit('passValue', this.value);
        }
    }
}

</script>

<style>
.slider-container {
    display: flex;
    width: 100%;
    align-items: center;
}
.left-bar, .right-bar, .slider {
    display: inline-block;
}
.left-bar, .right-bar {
    height: 5px;
}
.left-bar {
    background: #339966;
    flex-basis: 0;
    flex-grow: 0;
    flex-shrink: 0;
    border-radius: 2.5px 0 0 2.5px;
}
.slider {
    background: #339966;
    height: 30px;
    flex: 0 0 100px;
    border-radius: 5px;
    padding: 0 3px;
    cursor: grab;
    color: white;
    font-weight: 700;
    text-align: center;
    line-height: 30px;
    display: flex;
    justify-content: space-between;
}
.slider:hover {
    background-color: #2c8c54
}
.right-bar {
    background: #f8f8f8;
    flex: 1 1 auto;
    border-radius: 0 2.5px 2.5px 0;
}
.slider span {
    font-size: 14px;
}
</style>