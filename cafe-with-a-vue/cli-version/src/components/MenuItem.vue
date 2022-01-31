<script>
export default {
	name: "MenuItem",
	props: ["addToShoppingCart", "image", "inStock", "name", "price", "quantity"],
	data() {
		return {
			onSale: false
		}
	},
	computed: {
		generatedPrice() {
			if (this.onSale) { return(this.price * 0.9).toFixed(2)
			}else {
				return this.price
			}
		}
	},
	beforeMount() {
		const date = new Date()
		function numIsPair(n) { return (n & 1) ? false : true;}
		if (!numIsPair(date.getDate())) {
			this.onSale = true
		}
		console.log('Je vais bientot être monté sur le DOM', date.getDate());
	}
	
	
}
</script>

<template>
	<div class="menu-item">
		<img class="menu-item__image" :src="image.source" :alt="image.alt" />
		<div>
			<h3>{{ name }}</h3>
			<p>Prix : {{ generatedPrice }}</p>
			<p v-if="inStock">En stock</p>
			<p v-else>En rupture de stock</p>
			<div>
				<label for="add-item-quantity">Quantité : {{ quantity }}</label>
				<input v-model.number="quantity" id="add-item-quantity" type="number" />
				<button @click="addToShoppingCart(quantity)">
					Ajouter au panier
				</button>
			</div>
		</div>
	</div>
</template>

<style></style>
