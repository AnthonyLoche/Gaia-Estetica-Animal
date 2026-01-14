<script setup>
import HandWash from 'vue-material-design-icons/HandWash.vue';
import AccountSchoolOutline from 'vue-material-design-icons/AccountSchoolOutline.vue';
import HandHeartOutline from 'vue-material-design-icons/HandHeartOutline.vue';
</script>

<template>
    <section class="stacks">
        <div class="container">
            <div class="item">
                <div class="icon">
                    <HandHeartOutline />
                </div>
                <div class="text">
                    <div class="title">Paciência e Carinho</div>
                    <div class="desc">Respeitamos o tempo de cada pet, sem pressa ou estresse.</div>
                </div>
            </div>
            <div class="item">
                <div class="icon">
                    <HandWash />
                </div>
                <div class="text">
                    <div class="title">Higiene Rigorosa</div>
                    <div class="desc">Ambiente 100% esterelizado e produtos de linha profissional.</div>
                </div>
            </div>
            <div class="item">
                <div class="icon">
                    <AccountSchoolOutline />
                </div>
                <div class="text">
                    <div class="title">Profissionais Experts</div>
                    <div class="desc">Esteticistas animais certificados e em constante atualização</div>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.stacks {
    width: 100%;
    height: 30vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #F2F1E9;
    margin-top: 2rem;
}

.container {
    width: 90%;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    gap: 2rem;
}

.item {
    display: flex;
    align-items: center;
    gap: 1rem;
    flex: 1;
}

.icon {
    color: var(--color-primary);
    background-color: #c1c1c1;
    padding: 1rem;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
}

span {
    display: flex;
    align-items: center;
    justify-content: center;
}

.title {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--color-primary);
    margin-bottom: 0.5rem;
}

.desc {
    font-size: 1rem;
    color: #555555;
    width: 80%;
}
</style>