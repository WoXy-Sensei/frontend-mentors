<script setup></script>

<template>
    <div class="page">
        <div class="box">
            <div class="profile-image">
                <img src="./assets/images/avatar-jessica.jpeg" alt="" />
            </div>
            <div class="profile-content">
                <h1 class="profile-name">Jessica Randall</h1>
                <p class="profile-location">London, United Kingdom</p>
            </div>
            <div class="profile-description">
                <p>Front-end developer and avid reader.</p>
            </div>
            <div class="profile-buttons">
                <a href="#" class="button">GitHub</a>
                <a href="#" class="button">Frontend Mentor</a>
                <a href="#" class="button"> LinkedIn</a>
                <a href="#" class="button"> Twitter</a>
                <a href="#" class="button"> Instagram</a>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
$green: hsl(75, 94%, 57%);
$white: hsl(0, 0%, 100%);
$grey-700: hsl(0, 0%, 20%);
$grey-800: hsl(0, 0%, 12%);
$grey-900: hsl(0, 0%, 8%);

.page {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.box {
    background-color: $grey-800;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 3.2rem;
    border-radius: 1rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    gap: 2.2rem;
    .profile-image {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        overflow: hidden;

        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
    }

    .profile-content {
        text-align: center;
        display: flex;
        flex-direction: column;
        gap: 0.6rem;

        .profile-name {
            font-size: 2rem;
            font-weight: 600;
            color: $white;
        }

        .profile-location {
            color: $green;
            font-size: 16px;
            font-weight: 700;
        }
    }

    .profile-description {
        color: $white;
        opacity: 80%;
        font-weight: 400;
        display: flex;

        p {
            font-size: 16px;
        }

        &::before {
            content: '"';
        }

        &::after {
            content: '"';
        }
    }

    .profile-buttons {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 1rem;

        .button {
            width: 350px;
            text-align: center;
            background-color: $grey-700;
            color: $white;
            font-weight: 700;
            padding: 1rem 2rem;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: background-color 0.3s ease;

            &:hover {
                background-color: $green;
                color: #000;
            }
        }
    }
}

@media (max-width: 500px) {
    .box {
        padding: 1.5rem;
    }
    .box .profile-buttons .button {
        width: 300px;
    }
}

@media (max-width: 350px) {
    .box {
        padding: 1rem;
    }
    .box .profile-buttons .button {
        width: 280px;
    }

    .box .profile-description p {
        font-size: 14px;
    }
}
</style>
