<script>

let user = {
		id: "",
		name:  "",
		surname: "",
		adress: "",
		phone: "",
		email: "",
		rol: ""
	};

	let listado_usuarios = [];

	const guardarusers = () =>{
		user = listado_usuarios.push(user);
		console.log(user);
        console.log(listado_usuarios);
        resertformusers();

	};

    const resertformusers = () =>{
        user = {
            id: "",
            name:  "",
            surname: "",
            adress: "",
            phone: "",
            email: "",
			rol: ""
	    }
    }


	 let rol = {
        rol_name: ""
    }

    let listado_roles = [];


    const guardarroles = () =>{
        rol=listado_roles.push(rol);
        console.log(rol);
        console.log(listado_roles);
        resetform();
        
    }

    const resetform = () =>{
        rol = {
            rol_name: ""
        }
    }
</script>

<main>
	<div class="container mx-auto">
		<div class="grid grid-cols-2 gap-4">
			<div class="p-4 shadow-md rounded-md text-lef">
				<form on:submit|preventDefault={guardarusers}>
					<label for="name">Nombre</label>
					<input
						bind:value={user.name}
						id="name"
						type="text"
						placeholder="Inserte su nombre"
					/>
					<label for="surname">Apellidos</label>
					<input
						bind:value={user.surname}
						id="username"
						type="text"
						placeholder="Inserte sus apellidos"
					/>
					<label for="adress">Dirección</label>
					<input
						bind:value={user.adress}
						id="adress"
						type="text"
						placeholder="Inserte su dirección"
					/>
					<label for="phone">Teléfono</label>
					<input
						bind:value={user.phone}
						id="phone"
						type="text"
						placeholder="Inserte su número de teléfono"
					/>
					<label for="email">Correo Electrónico</label>
					<input
						bind:value={user.email}
						id="email"
						type="text"
						placeholder="Inserte su correo electrónico"
					/>
					<label for="rol">Rol</label>
					<select bind:value={user.rol} id="rol">
						{#each listado_roles as r}
						<option value={r.rol_name}>
							{r.rol_name}
						</option>
						{/each}
					</select>
					<button>
						Guardar Usuario
					</button>
				</form>
			</div>
		</div>
	</div>
		<div class="p-4 shadow-md rounded-md text-center">
			<form on:submit|preventDefault={guardarroles}>
				<label for="namerol">Nombre del Rol: </label>
				<input
					bind:value={rol.rol_name}
					type="text"
					id="rol"
					placeholder="Inserte el nombre del rol"
				>
				<button>
					Guardar
				</button>
			</form>
		</div>

</main>
