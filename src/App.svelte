<script>

					//Database
//---------------------------------------------------------

import {db} from "../src/firebase";

import{
	collection,
	getDocs,
	doc,
	addDoc,
	updateDoc,
	deleteDoc,
}
from "firebase/firestore";

//-------------------------------------------------------------------------

	let editar = false;

//--------------------------------------------------------------------------
				//Users

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

	const cgDatosus = async() =>{
		const querySnapshot = await getDocs(collection(db, "user"));
		let user = [];
		querySnapshot.forEach((doc) => {
			docs.push({...doc.data(), id: doc.id});
		});
		listado_usuarios = [...docs];
		console.log(listado_usuarios);
	};
	cgDatosus();

	const subir_Users = async() => {
		await addDoc(collection(db, "user"), user);
		await cgDatosus();
		await resertformusers();
	}

	const deleteUser = async(id) => {
		await deleteDoc(doc(db, "user", id));
		await cgDatosus();
	}

	const editUser = (u) => {
		user = Object.assign({}, d.user);
		editar = true;
	}


	// const guardarusers = () =>{
	// 	user = listado_usuarios.push(user);
	// 	console.log(user);
    //     console.log(listado_usuarios);
    //     resertformusers();

	// };

//-------------------------------------------------------------------------------------------------
			//Roles
	 let rol = {
        rol_name: ""
    }

    let listado_roles = [];

	const resetform = () =>{
        rol = {
            rol_name: ""
        }
    }

	const cgDatoR = async() =>{
		const querySnapshot = await getDocs(collection(db, "rol"));
		let rol = [];
		querySnapshot.forEach((doc) => {
			docs.push({...doc.data(), id: doc.id});
	});
	listado_roles = [...docs];
	console.log(listado_roles);
};
cgDatoR();

	const subir_Roles = async() => {
		await addDoc(collection(db, "rol"), rol);
		await cgDatoR();
		resetform();
	};

    // const guardarroles = () =>{
    //     rol=listado_roles.push(rol);
    //     console.log(rol);
    //     console.log(listado_roles);
    //     resetform();
        
    // }


	
</script>

<main>
	<div class="container mx-auto">
		<div class=" grid grid-cols-2 gap-4">
			<!-- //listado_usuarios -->
			<div class="bg-gray-100 grid grid-cols-1 gap-6">
				{#each listado_usuarios as u, i}
				<div class="w-full md:w-3/5 text-left p-6 md:p-4 space-y-2">
					<div class="text-xl text-gray-700 font-bold">
						{u.name}
					</div>
					<div class="text-xl text-gray-700 font-bold">
						{u.surname}
					</div>
					<div class="text-xl text-gray-700 font-bold">
						{u.adress}
					</div>
					<div class="text-xl text-gray-700 font-bold">
						{u.phone}
					</div>
					<div class="text-xl text-gray-700 font-bold">
						{u.email}
					</div>
					<div class="text-xl text-gray-700 font-bold">
						{u.rol}
					</div>
					<button
							
									on:click={editUser(u)}
									><svg
										xmlns="http://www.w3.org/2000/svg"
										class="h-6 w-6"
										fill="none"
										viewBox="0 0 24 24"
										stroke="currentColor"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											stroke-width="2"
											d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
										/>
									</svg>
								</button>
				</div>
			</div>
		</div>
		<div class="p-4 shadow-md rounded-md text-lef">
			<form on:submit|preventDefault={subir_Users}>
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
		<div class="p-4 shadow-md rounded-md text-center">
			<form on:submit|preventDefault={subir_Roles}>
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
	</div>
</main>
