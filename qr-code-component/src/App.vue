<script setup></script>

<template>
    <div class="page">
        <div class="qrcode-component">
            <div class="qr-image">
                <img src="/image-qr-code.png" alt="" />
            </div>
            <div class="content">
                <div class="title">
                    Improve your front-end skills by building projects
                </div>
                <div class="description">
                    Scan the QR code to visit Frontend Mentor and take your
                    coding skills to the next level
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.page {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: var(--slate-300);
}

.qrcode-component {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 1.2rem;
    border-radius: 1rem;
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
    background-color: var(--white);

    width: 350px;
}

.qrcode-component .qr-image {
    margin-bottom: 1rem;
    width: 100%;
    border-radius: 1rem;
    overflow: hidden;

    img {
        width: 100%;
        height: auto;
    }
}
.qrcode-component .content {
    text-align: center;
    padding: 1.2rem;
}

.qrcode-component .content .title {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 1rem;
}

.qrcode-component .content .description {
    font-size: 1rem;
    color: var(--slate-500);
    line-height: 1.5;
}
</style>
