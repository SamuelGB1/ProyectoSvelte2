<script>
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
</main>
