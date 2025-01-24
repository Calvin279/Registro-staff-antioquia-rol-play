<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro de Asistencia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
</head>
<body class="bg-gray-100 font-roboto">
    <div class="container mx-auto p-4">
        <h1 class="text-3xl font-bold text-center mb-6">Registro de Asistencia</h1>
        
        <div class="bg-white p-6 rounded-lg shadow-lg mb-6">
            <h2 class="text-2xl font-bold mb-4">Registrar Entrada/Salida</h2>
            <form id="registroForm" class="space-y-4">
                <div>
                    <label for="nombre" class="block text-sm font-medium text-gray-700">Nombre</label>
                    <input type="text" id="nombre" name="nombre" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" required>
                </div>
                <div>
                    <label for="rango" class="block text-sm font-medium text-gray-700">Rango</label>
                    <input type="text" id="rango" name="rango" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" required>
                </div>
                <div>
                    <label for="horaEntrada" class="block text-sm font-medium text-gray-700">Hora de Entrada</label>
                    <input type="time" id="horaEntrada" name="horaEntrada" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" required>
                </div>
                <div>
                    <label for="horaSalida" class="block text-sm font-medium text-gray-700">Hora de Salida</label>
                    <input type="time" id="horaSalida" name="horaSalida" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" required>
                </div>
                <button type="button" onclick="registrar()" class="w-full bg-indigo-600 text-white p-2 rounded-md shadow-md hover:bg-indigo-700">Registrar</button>
            </form>
        </div>

        <div class="bg-white p-6 rounded-lg shadow-lg">
            <h2 class="text-2xl font-bold mb-4">Buscar Registros</h2>
            <form id="buscarForm" class="space-y-4">
                <div>
                    <label for="buscarNombre" class="block text-sm font-medium text-gray-700">Nombre</label>
                    <input type="text" id="buscarNombre" name="buscarNombre" class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                </div>
                <button type="button" onclick="buscar()" class="w-full bg-indigo-600 text-white p-2 rounded-md shadow-md hover:bg-indigo-700">Buscar</button>
            </form>
        </div>

        <div id="resultados" class="mt-6">
            <!-- Resultados de la búsqueda aparecerán aquí -->
        </div>
    </div>

    <script>
        // Simulando una base de datos en memoria
        const registros = [];

        function registrar() {
            const nombre = document.getElementById('nombre').value;
            const rango = document.getElementById('rango').value;
            const horaEntrada = document.getElementById('horaEntrada').value;
            const horaSalida = document.getElementById('horaSalida').value;

            if (!nombre || !rango || !horaEntrada || !horaSalida) {
                alert("Por favor, complete todos los campos.");
                return;
            }

            const registro = {
                nombre,
                rango,
                horaEntrada,
                horaSalida,
                fecha: new Date().toLocaleDateString()
            };

            registros.push(registro);
            alert("Registro guardado exitosamente.");
            document.getElementById('registroForm').reset();
        }

        function buscar() {
            const buscarNombre = document.getElementById('buscarNombre').value;
            const resultadosDiv = document.getElementById('resultados');
            resultadosDiv.innerHTML = ''; // Limpiar resultados anteriores

            const resultados = registros.filter(registro => registro.nombre.toLowerCase().includes(buscarNombre.toLowerCase()));

            if (resultados.length === 0) {
                resultadosDiv.innerHTML = '<p class="text-gray-500">No se encontraron registros.</p>';
                return;
            }

            const listaResultados = document.createElement('ul');
            listaResultados.className = 'space-y-2';

            resultados.forEach(registro => {
                const listItem = document.createElement('li');
                listItem.className = 'bg-gray-200 p-4 rounded-md shadow-sm';
                listItem.innerHTML = `
                    <strong>Nombre:</strong> ${registro.nombre}<br>
                    <strong>Rango:</strong> ${registro.rango}<br>
                    <strong>Hora de Entrada:</strong> ${registro.horaEntrada}<br>
                    <strong>Hora de Salida:</strong> ${registro.horaSalida}<br>
                    <strong>Fecha:</strong> ${registro.fecha}
                `;
                listaResultados.appendChild(listItem);
            });

            resultadosDiv.appendChild(listaResultados);
        }
    </script>
</body>
</html>
