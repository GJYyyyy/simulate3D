<template>
    <div class="simulate-3-d" @mousedown="onMouseDown" @mouseup="onMouseUp" @mousemove="onMouseMove"
        @mouseleave="onMouseLeave" @wheel="onMouseWheel" @contextmenu="(ev) => ev.preventDefault()">
        <div class="visual-effect"
            :style="`--rotateX: ${rotateX}deg; --rotateY: ${rotateY}deg; --translateX: ${translateX}px; --translateY: ${translateY}px; --scale: ${scale};`">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    data: () => ({
        isRotating: false,
        isMoving: false,

        rotateX: 10,
        rotateY: 0,
        translateX: 0,
        translateY: 0,
        scale: 1,
    }),
    methods: {
        reset() {
            this.rotateX = 10;
            this.rotateY = 0;
            this.translateX = 0;
            this.translateY = 0;
            this.scale = 1;
        },
        onMouseDown(ev) {
            if (ev.button === 0) {
                this.isRotating = true;
            } else if (ev.button === 2) {
                this.isMoving = true;
            }
        },
        onMouseLeave() {
            this.isRotating = false;
            this.isMoving = false;
        },
        onMouseUp() {
            this.isRotating = false;
            this.isMoving = false;
        },
        onMouseMove(ev) {
            if (this.isRotating) {
                let unitNum = 0.2,
                    minDeg = -80,
                    maxDeg = 80;

                this.rotateY += unitNum * ev.movementX;
                this.rotateX -= unitNum * ev.movementY;

                if (this.rotateY < minDeg) this.rotateY = minDeg;
                if (this.rotateY > maxDeg) this.rotateY = maxDeg;
                if (this.rotateX < minDeg) this.rotateX = minDeg;
                if (this.rotateX > maxDeg) this.rotateX = maxDeg;
            } else if (this.isMoving) {
                let maxTranslateX = document.body.clientWidth / 4,
                    maxTranslateY = document.body.clientHeight / 4;

                this.translateX += ev.movementX;
                this.translateY += ev.movementY;

                if (this.translateX > maxTranslateX) this.translateX = maxTranslateX;
                if (this.translateX < -maxTranslateX) this.translateX = -maxTranslateX;
                if (this.translateY > maxTranslateY) this.translateY = maxTranslateY;
                if (this.translateY < -maxTranslateY) this.translateY = -maxTranslateY;
            }
        },
        onMouseWheel(ev) {
            let minScale = 0.3,
                maxScale = 1.8;

            if (ev.deltaY < 0) {
                this.scale *= 1.1;
            } else {
                this.scale *= 0.9;
            }

            if (this.scale < minScale) this.scale = minScale;
            if (this.scale > maxScale) this.scale = maxScale;
        },
    },
};
</script>

<style scoped lang="scss">
.simulate-3-d {
    >.visual-effect {
        transform: perspective(800px) rotateX(var(--rotateX)) rotateY(var(--rotateY)) scale(var(--scale)) translate(var(--translateX), var(--translateY));
    }
}
</style>