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
	    };
		editar = false;
    }

	const cgDatosus = async () => {
		const querySnapshot = await getDocs(collection(db, "user"));
		let docs = [];
		querySnapshot.forEach((doc) => {
			docs.push({ ...doc.data(), id: doc.id });
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
		user = Object.assign({}, u);
		editar = true;
	}

	const updateuser = async () =>{
		await updateDoc(collection(db, "user"), user);
		await cgDatosus();
		await resertformusers();

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
        };
		editar = false;
    }

	const cgDatoR = async () => {
		const querySnapshot = await getDocs(collection(db, "rol"));
		let docs = [];
		querySnapshot.forEach((doc) => {
			docs.push({ ...doc.data(), id: doc.id });
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
		<h1>Usuarios y Roles</h1>
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
						class="ml-5 bg-blue-200 py-1 px-2 border border-blue-500 rounded-md shadow-sm text-sm leading-4 font-medium text-gray-700 hover:bg-blue-500 hover:text-gray-100 focus:ring-2 focus:ring-offset-2 focus:ring-blue-300 focus:text-gray-700 focus:bg-blue-200"
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
					<button
									class="ml-5 bg-red-200 py-1 px-2 border border-red-500 rounded-md shadow-sm text-sm leading-4 font-medium text-gray-700 hover:bg-red-500 hover:text-gray-100 focus:ring-2 focus:ring-offset-2 focus:ring-red-300 focus:text-gray-700 focus:bg-red-200"
									on:click={deleteUser(u.id)}
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
											d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
										/>
									</svg>
					</button>
					<button class="uppercase p-3 flex items-center bg-yellow-500 text-blue-50 max-w-max shadow-sm hover:shadow-lg rounded-full w-12 h-12 " on:click={updateuser()}>
						<svg  width="32" height="32" preserveAspectRatio="xMidYMid meet" viewBox="0 0 32 32" style="transform: rotate(360deg);"><path d="M26 18A10 10 0 1 1 16 8h6.182l-3.584 3.585L20 13l6-6l-6-6l-1.402 1.414L22.185 6H16a12 12 0 1 0 12 12z" fill="currentColor"></path></svg>
						</button>
				</div>
				{/each}			
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
