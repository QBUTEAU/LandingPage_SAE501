<template>
    <div class="avancee" id="avancee">
        <h2>AVANCÉE DU PROJET</h2>

        <p>À l'heure actuelle, le menu du jeu est opérationel, permettant un accès direct au jeu, de le quitter
            ou bien de voir les 10 meilleurs scores du jeu. Les deux personnages sont jouables, avec des animations
            idle - jump - run. Lorsque qu'un personnage sort du cadre de jeu, la partie se termine et l'écriture du
            pseudonyme du vainqueur est demandée. Une fois ajouté, les 10 meilleurs scores mis à jour s'affichent,
            avec le nouveau score si celui-ci est suffisant pour être dans le top 10, puis il faut revenir au menu
            et relancer une partie pour rejouer.
        </p>

        <p>Actuellement, nous créons un système de maps aléatoires, nous ajoutons des power-ups et des obstacles ainsi que
            leurs animations pouvant jouer en la faveur de l'un et la défaveur de l'autre, une animation lors de
            la victoire d'un joueur différente selon le personnage et un compte à rebord avant le début de la partie.
            Nous sommes également en pleine création d'une Attract Mode, qui aura pour but d'attirer les futurs joueurs.
        </p>
        <p class="avancee-maj">Mis à jour le 25/11/2024 à 11h26</p>
    </div>
</template>

<script>
export default {
    name: 'Avancee'
}
</script>