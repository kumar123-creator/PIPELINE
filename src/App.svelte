<script>
	import { onMount } from "svelte";
	import "bootstrap/dist/css/bootstrap.min.css";
  
	let todos = [];
	let selectedTodo = null; // To keep track of the selected todo
  
	onMount(async () => {
	  try {
		const response = await fetch(
		  "https://api.recruitly.io/api/job/pipeline/byjob?apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77&jobApplication=false&jobId=testeb576ee7159440dc91364446af47d696&rejected=false"
		);
		const data = await response.json();
		console.log(data);
		if (Array.isArray(data)) {
		  todos = data.map((item) => ({
			candidateRef: item.candidateRef,
			candidateLabel: item.candidateLabel,
			candidateEmail: item.candidateEmail,
			candidatePhone: item.candidatePhone,
			candidateOwner: item.candidateOwner,
		  }));
		} else {
		  console.error("API response is not in the expected format");
		}
	  } catch (error) {
		console.error(error);
	  }
	});
  
	function showDetails(todo) {
	  selectedTodo = todo;
	}
  </script>
  
  <div class="table-responsive">
	<div class="table">
	  <div class="horizontal-table">
		<div class="card">
		  <label class="card-title text-primary" for="shortlisted">Shortlisted</label>
		  {#each todos.filter((todo) => todo.status === 0) as todo, index}
		  <div class="vertical-table">
			<div class="card">
			  <p>{todo.candidateRef}</p>
			  <p>
				<a href="#Job_pipeline" on:click={() => showDetails(todo)}>
				  {todo.candidateLabel}
				</a>
			  </p>
			  <p>{todo.candidateEmail}</p>
			  <p>{todo.candidatePhone}</p>
			</div>
		  </div>
		  {/each}
		</div>
  
		<div class="card">
			<label class="card-title text-primary" for="sourced">Sourced</label>
			{#each todos.filter((todo) => todo.status === 1) as todo, index}
			<div class="vertical-table">
			  <div class="card">
				<p>{todo.candidateRef}</p>
				<p>
				  <a href="#Job_pipeline" on:click="{() => showDetails(todo)}">{todo.candidateLabel}</a>
				</p>
				<p>{todo.candidateEmail}</p>
				<p>{todo.candidatePhone}</p>
			  </div>
			</div>
			{/each}
		  </div>

		  <div class="card">
			<label class="card-title text-primary" for="applied">Applied</label>
			{#each todos.filter((todo) => todo.status === 2) as todo, index}
			<div class="vertical-table">
			  <div class="card">
				<p>{todo.candidateRef}</p>
				<p>
				  <a href="#Job_pipeline" on:click="{() => showDetails(todo)}">{todo.candidateLabel}</a>
				</p>
				<p>{todo.candidateEmail}</p>
				<p>{todo.candidatePhone}</p>
			  </div>
			</div>
			{/each}
		  </div>

		  <div class="card">
			<label class="card-title text-primary" for="cv shared">CV Shared</label>
			{#each todos.filter((todo) => todo.status === 3) as todo, index}
			<div class="vertical-table">
			  <div class="card">
				<p>{todo.candidateRef}</p>
				<p>
				  <a href="#Job_pipeline" on:click="{() => showDetails(todo)}">{todo.candidateLabel}</a>
				</p>
				<p>{todo.candidateEmail}</p>
				<p>{todo.candidatePhone}</p>
			  </div>
			</div>
			{/each}
		  </div>

		  <div class="card">
			<label class="card-title text-primary" for="interview">Interview</label>
			{#each todos.filter((todo) => todo.status === 4) as todo, index}
			<div class="vertical-table">
			  <div class="card">
				<p>{todo.candidateRef}</p>
				<p>
				  <a href="#Job_pipeline" on:click="{() => showDetails(todo)}">{todo.candidateLabel}</a>
				</p>
				<p>{todo.candidateEmail}</p>
				<p>{todo.candidatePhone}</p>
			  </div>
			</div>
			{/each}
		  </div>

		  <div class="card">
			<label class="card-title text-primary" for="offer">Offer</label>
			{#each todos.filter((todo) => todo.status === 5) as todo, index}
			<div class="vertical-table">
			  <div class="card">
				<p>{todo.candidateRef}</p>
				<p>
				  <a href="#Job_pipeline" on:click="{() => showDetails(todo)}">{todo.candidateLabel}</a>
				</p>
				<p>{todo.candidateEmail}</p>
				<p>{todo.candidatePhone}</p>
			  </div>
			</div>
			{/each}
		  </div>

	  </div>
	</div>
  </div>
  
  {#if selectedTodo}
  <div class="popup">
	<h1 class="left-align" style="color: darkblue;">Name:</h1>
	<p class="popup-text-top" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidateLabel}
	</p>
	<h1 class="left-align" style="color: darkblue;">Reference:</h1>
	<p class="popup-text" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidateRef}
	</p>
	<h1 class="left-align" style="color: darkblue;">ID:</h1>
	<p class="popup-text" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidateId}
	</p>
  
	<h1 class="left-align" style="color: darkblue;">Owner Name:</h1>
	<p class="popup-text" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidateOwner}
	</p>
	<h1 class="left-align" style="color: darkblue;">Phone:</h1>
	<p class="popup-text" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidatePhone}
	</p>
	<h1 class="left-align" style="color: darkblue;">Email:</h1>
	<p class="popup-text-bottom" style="font: 1.3em sans-serif;">
	  {selectedTodo.candidateEmail}
	</p>
	<button class="btn btn-primary" on:click={() => (selectedTodo = null)}>
	  Close
	</button>
  </div>
  {/if}
  
  <style>
	.left-align {
	  text-align: left;
	  font: 1.5em sans-serif;
	}
  
	.card {
	  margin: 10px;
	  padding: 10px;
	  border: 1px solid #ccc;
	  border-radius: 5px;
	  width: 150px;
	}
  
	.horizontal-table {
	  display: flex;
	  flex-direction: row;
	  overflow-x: auto;
	}
  
	.vertical-table {
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	}
  
	.popup {
	  position: fixed;
	  top: 50%;
	  left: 50%;
	  transform: translate(-50%, -50%);
	  background-color: #f6f3f4;
	  padding: 5px;
	  border-radius: 5px;
	  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
	  z-index: 999;
	  height: 80vh;
	  width: 60vh;
	}
  </style>
  