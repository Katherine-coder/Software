using System;
using System.Collections;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data.MySqlClient;

namespace TallerLemus.Clases
{
    public class CRUD
    {
        //instertar clientes
        public static int Agregar(Cliente cliente)
        {

            int retorno = 0;

            MySqlCommand comando = new MySqlCommand(string.Format("Insert into cliente (Nombre, Apellido, Direccion, Telefono, Correo) values ('{0}','{1}','{2}','{3}', '{4}')",
             cliente.Nombre, cliente.Apellido, cliente.Direccion, cliente.Telefono, cliente.Correo), conexion.obtenerconexion());
            retorno = comando.ExecuteNonQuery();
            return retorno;
        }

        //agregar autos
        public static int AgregarAut(Auto auto)
        {

            int retorno = 0;

            MySqlCommand comando = new MySqlCommand(string.Format("Insert into vehiculo (Matricula, Propietario, Modelo, Anio, NoVIN) values ('{0}','{1}','{2}','{3}','{4}')",
             auto.Matricula, auto.Propietario, auto.Modelo, auto.Anio, auto.NoVIN), conexion.obtenerconexion());
            retorno = comando.ExecuteNonQuery();
            return retorno;
        }

        //mostrar la informacion en el dtg
        public static Cliente Obtener(int pId)
        {
            Cliente cliente = new Cliente();
            MySqlConnection conectar = conexion.obtenerconexion();

            MySqlCommand _comando = new MySqlCommand(String.Format("SELECT IDCliente, Nombre, Apellido, Direccion, Telefono, Correo FROM cliente where IDCliente={0}", pId), conectar);
            MySqlDataReader _reader = _comando.ExecuteReader();
            while (_reader.Read())
            {
                cliente.IDCliente = _reader.GetInt32(0);
                cliente.Nombre = _reader.GetString(1);
                cliente.Apellido = _reader.GetString(2);
                cliente.Direccion = _reader.GetString(3);
                cliente.Telefono = _reader.GetInt32(4);
                cliente.Correo = _reader.GetString(5);

            }

            conectar.Close();
            return cliente;

        }

    }
}
