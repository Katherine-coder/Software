using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data.MySqlClient; 

namespace TallerLemus.Clases
{
    class conexion
    {
        public static MySqlConnection obtenerconexion()
        {
            MySqlConnection conexion = new MySqlConnection("server=localhost;database=taller;" +
                "Uid=root;pwd=;");
            conexion.Open();
            return conexion;
        }
    }
}
