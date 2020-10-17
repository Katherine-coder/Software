using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;
using TallerLemus.Clases;

namespace TallerLemus
{
    public partial class Clientes : Form
    {
        public Clientes()
        {
            InitializeComponent();
        }

        public Cliente Seleccionado { get; set; }
        public Cliente clienteActual { get; set; }

        private void btnGuardar_Click(object sender, EventArgs e)
        {

            if (txtNombre.Text == "" || txtApellido.Text == "" ||
                txtTelefono.Text == "" || txtDireccion.Text == "" || txtCorreo.Text == "")
            {
                MessageBox.Show("FALTA INFORMACIÓN");
            }
            else
            {

                Cliente cliente = new Cliente();
                cliente.Nombre = txtNombre.Text.Trim();
                cliente.Apellido = txtApellido.Text.Trim();
                cliente.Direccion = txtDireccion.Text.Trim();
                cliente.Telefono = int.Parse(txtTelefono.Text);
                cliente.Correo = txtCorreo.Text.Trim();

                int resultado = CRUD.Agregar(cliente);
                if (resultado > 0)
                {
                    MessageBox.Show("Cliente Guardado Con Exito!!", "Guardado", MessageBoxButtons.OK, MessageBoxIcon.Information);
                    txtNombre.Clear();
                    txtDireccion.Clear();
                    txtApellido.Clear();
                    txtCorreo.Clear();
                    txtTelefono.Clear();
                    
                }
                else
                {
                    MessageBox.Show("No se pudo guardar el cliente", "Fallo!!", MessageBoxButtons.OK, MessageBoxIcon.Exclamation);
                }
            }
        }
    }
}

