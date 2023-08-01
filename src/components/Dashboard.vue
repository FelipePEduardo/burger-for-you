<template>
	<div id="burger-table">
		<Message :msg="msg" v-show="msg" />
		<div>
			<div id="burger-table-heading">
				<div class="order-id">#:</div>
				<div>Cliente:</div>
				<div>Pão:</div>
				<div>Carne:</div>
				<div>Opcionais:</div>
				<div>Ações:</div>
			</div>
		</div>
		<div id="burger-table-rows" v-for="burger in burgersList" :key="burger.id">
			<div class="burger-table-row">
				<div class="order-number">{{ burger.id }}</div>
				<div>{{ burger.name }}</div>
				<div>{{ burger.bread }}</div>
				<div>{{ burger.meat }}</div>
				<div>
					<ul>
						<li v-for="option in burger.optional" :key="option">
							{{ option }}
						</li>
					</ul>
				</div>
				<div>
					<select
						name="status"
						class="status"
						@change="updateBurger($event, burger.id)"
					>
						<option>Selecione</option>
						<option
							v-for="s in status"
							:key="s.id"
							:value="s.type"
							:selected="burger.status == s.type"
						>
							{{ s.type }}
						</option>
					</select>
					<button class="delete-btn" @click="deleteBurger(burger.id)">
						Cancelar
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script setup>
import Message from './Message.vue'

import { ref, onMounted } from 'vue'

/* #region Data */

const burgersList = ref([])
const status = ref([])
const msg = ref('')

/* #endregion */

/* #region Methods */

async function getStatus() {
	const req = await fetch('http://localhost:3000/status')
	const data = await req.json()

	status.value = data
}

async function getRequests() {
	const res = await fetch('http://localhost:3000/burgers')
	const data = await res.json()

	burgersList.value = data

	getStatus()
}

async function deleteBurger(id) {
	const res = await fetch(`http://localhost:3000/burgers/${id}`, {
		method: 'DELETE'
	})
	await res.json()

	msg.value = `Pedido N° ${id} removido com sucesso!`

	setTimeout(() => (msg.value = ''), 3000)

	getRequests()
}

async function updateBurger(e, id) {
	const statusJSON = JSON.stringify({ status: e.target.value })

	const res = await fetch(`http://localhost:3000/burgers/${id}`, {
		method: 'PATCH',
		headers: { 'Content-Type': 'application/json' },
		body: statusJSON
	})

	const data = await res.json()

	msg.value = `Pedido N° ${id} atualizado para ${data.status}!`

	setTimeout(() => (msg.value = ''), 3000)
}

/* #endregion */

/* #region Life Cycle */

onMounted(getRequests)

/* #endregion */
</script>

<style scoped>
#burger-table {
	max-width: 1200px;
	margin: 0 auto;
	padding: 20px;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
	display: flex;
	flex-wrap: wrap;
}

#burger-table-heading {
	font-weight: bold;
	padding: 12px;
	border-bottom: 3px solid #333;
}

.burger-table-row {
	width: 100%;
	padding: 12px;
	border-bottom: 1px solid #ccc;
}

#burger-table-heading div,
.burger-table-row div {
	width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
	width: 5%;
}

select {
	padding: 12px 6px;
	margin-right: 12px;
}

.delete-btn {
	background-color: #222;
	color: #fcba03;
	font-weight: bold;
	border: 2px solid #222;
	padding: 10px;
	font-size: 16px;
	margin: 0 auto;
	cursor: pointer;
	transition: 0.5s;
}

.delete-btn:hover {
	background-color: transparent;
	color: #222;
}
</style>
