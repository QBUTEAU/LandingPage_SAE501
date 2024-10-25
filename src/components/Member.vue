<template>
    <li class="member">
        <div class="member__img" :class="member.className"></div>
        <div class="member__nom">
            <h3>{{ member.name }}</h3>
            <p>{{ member.role }}</p>
            <div class="member__links">
                <a :href="member.portfolio" target="_blank" class="portfolio-link">
                    <i class="fa-solid fa-link"></i>
                </a>
                <a :href="member.github" target="_blank" class="github-link">
                    <i class="fa-brands fa-github"></i>
                </a>
            </div>
        </div>
    </li>
</template>

<script>
export default {
    name: 'Member',
    props: {
        member: {
            type: Object,
            required: true
        }
    }
}
</script>

<style>
.member__links {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 10px;
}

.member__links a i {
    font-size: 20px;
    color: #F1F1F1;
}
</style>