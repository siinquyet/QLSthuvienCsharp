using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Drawing;
using System.Runtime.CompilerServices;
using System.Security.Policy;
using System.ComponentModel.Design;
using System.ComponentModel;
using System.IO;
using System.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;

namespace BaiTapNhom
{
    
    
    internal class Program
    {
        static void ThemSach()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
            Console.WriteLine($"│{"                 Chức năng thêm sách",-60}│");
            Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
            Console.Write(" [Add]Tên sách: ");
            string tensach = Console.ReadLine();
            Console.Write(" [Add]ID sách: ");
            int idsach = int.Parse(Console.ReadLine());       
            Console.Write(" [Add]Tác giả: ");
            string tacgia = Console.ReadLine();
            Console.Write(" [Add]Thể loại: ");
            string theloai = Console.ReadLine();
            Console.Write(" [Add]Giá sách: ");
            int giasach = int.Parse(Console.ReadLine());
            Console.Write(" [Add]Số lượng: ");
            byte soluong = byte.Parse(Console.ReadLine());
            string insertQuery = "INSERT INTO Sach (IDSach,TenSach,TacGia,TheLoai,GiaSach,SoLuong) VALUES('" + idsach + "',N'" + tensach + "',N'"+ tacgia + "',N'" + theloai + "'," + giasach + "," +soluong + ")";
            SqlCommand Insert = new SqlCommand(insertQuery, conn);
            Insert.ExecuteNonQuery();
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("\n [✔️]Hoàn Thành!!!");
            Console.ResetColor();
            Console.WriteLine("══════════════════════════════════════════════════════════════");
            conn.Close();
            GoBack();

        }
        static void XoaSach()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM Sach";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
            Console.WriteLine($"│{"                 Chức năng xóa sách",-60}│");
            Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
            Console.Write("\n [Delete] Nhập ID Sach: ");
            int Timkiem = Convert.ToInt32(Console.ReadLine());
            for (int i = 0; i < dataReader.FieldCount; i++)
            {
                if (dataReader.Read())
                {
                    
                    if (Timkiem == dataReader.GetInt32(0))
                    {
                        //xóa user trong danh sach
                        dataReader.Close();
                        string deleteQuery = "DELETE FROM Sach WHERE IDSach =" + Timkiem;
                        SqlCommand deleteCommand = new SqlCommand(deleteQuery, conn);
                        deleteCommand.ExecuteNonQuery(); 
                        conn.Close();
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("\n [✔️]Hoàn Thành!!!");
                        Console.ResetColor();
                        Console.WriteLine("══════════════════════════════════════════════════════════════");
                        GoBack();
                        break;
                    }
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine(" \n\n[❌] ID Sách không tồn tại !!!\n");
                    Console.ResetColor();
                    Console.WriteLine("══════════════════════════════════════════════════════════════");
                    conn.Close();
                    GoBack();
                }
            }

        }
        static void ChinhSua()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM Sach";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
            Console.WriteLine($"│{"         Chức năng chỉnh sửa thông tin sách",-60}│");
            Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
            Console.Write("Nhập ID Sách:");
            int Timkiem = Convert.ToInt32(Console.ReadLine());
            for (int i = 0; i < dataReader.FieldCount; i++)
            {
                if (dataReader.Read())
                {

                    if (Timkiem == dataReader.GetInt32(0))
                    {

                        dataReader.Close();
                        Console.Write("[Update]Tên sách: ");
                        string tensach = Console.ReadLine();
                        Console.Write("[Update]Tác giả: ");
                        string tacgia = Console.ReadLine();
                        Console.Write("[Update]Thể loại: ");
                        string theloai = Console.ReadLine();
                        Console.Write("[Update]Giá sách: ");
                        int giasach = int.Parse(Console.ReadLine());
                        Console.Write("[Update]Số lượng: ");
                        byte soluong = byte.Parse(Console.ReadLine());
                        string updateQuery = "UPDATE Sach SET TenSach = '" + tensach + "',TacGia ='" + tacgia + "',TheLoai ='" + theloai + "',GiaSach=" + giasach + ",SoLuong=" + soluong + "WHERE IDSach =" + Timkiem + "";
                        SqlCommand updateCommand = new SqlCommand(updateQuery, conn);
                        updateCommand.ExecuteNonQuery();
                        conn.Close();
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("\n[✔️]Hoàn Thành !!!");
                        Console.ResetColor();
                        Console.WriteLine("══════════════════════════════════════════════════════════════");
                        GoBack();
                        break;
                    }
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine(" \n\n[❌] ID Sách không tồn tại !!!\n");
                    Console.ResetColor();
                    Console.WriteLine("══════════════════════════════════════════════════════════════");
                    conn.Close();
                    GoBack();
                }
            }
        }
        static void DSSach()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM Sach";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌——————————┬——————————————————————————————┬————————————————————┬——————————————————————————————┬——————————┬————————┐");
            Console.WriteLine($"│{"ID Sách",-10}│{"Tên sách",-30}│{"Tác giả",-20}│{"Thể loại",-30}│{"Giá sách",-10}│{"Số lượng",-8}│");
            Console.WriteLine("├——————————┼——————————————————————————————┼————————————————————┼——————————————————————————————┼——————————┼———---——┤");
            for (int i = 0; i < dataReader.FieldCount; i++) 
            {
                if(dataReader.Read())
                {
                    Console.Write($"│{dataReader.GetValue(0),-10}");
                    Console.Write($"│{dataReader.GetValue(1),-30}");
                    Console.Write($"│{dataReader.GetValue(2),-20}");
                    Console.Write($"│{dataReader.GetValue(3),-30}");
                    Console.Write($"│{dataReader.GetValue(4),-10}");
                    Console.WriteLine($"│{dataReader.GetValue(5),-8}│");
                }
                
            }
            Console.WriteLine("┗——————————————————————————————————————————————————————————————————————————————————————————————————————————————-——┚");
            dataReader.Close();
            conn.Close();
            GoBack();

        }   
        static void DSMuonTra()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM DSMuonTra";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌————————————————————┬———————————————┬——————————————————————————————┬————————————┬———————————————┬———————————————┐");
            Console.WriteLine($"│{"Tên Đọc Giả",-20}│{"Liên Hệ",-15}│{"Địa Chỉ",-30}│{"ID Sách Mượn",-12}│{"Ngày Mượn",-15}│{"Ngày Trả",-15}│");
            Console.WriteLine("├————————————————————┼——————————————-┼——————————————————————————————┼————————————┼———————————————┼———————————————┤");
            for (int i = 0; i < dataReader.FieldCount; i++)
            {
                if (dataReader.Read())
                {
                    Console.Write($"│{dataReader.GetValue(0),-20}");
                    Console.Write($"│{dataReader.GetValue(1),-15}");
                    Console.Write($"│{dataReader.GetValue(2),-30}");
                    Console.Write($"│{dataReader.GetValue(3),-12}");
                    Console.Write($"│{dataReader.GetValue(4),-15}");
                    Console.WriteLine($"│{dataReader.GetValue(5),-15}│");
                }


            }
            Console.WriteLine("┗—————————————————————————————————————————————————————————————————————————————————————————————————————————————-——┚");
            dataReader.Close();
            conn.Close();
            GoBack();
        }
        static void TraSach()
        {
            
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM DSMuonTra";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
            Console.WriteLine($"│{"                Chức năng trả sách",-60}│");
            Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
            Console.Write("\n[Trả Sách] Nhập SDT:");
            int Timkiem = Convert.ToInt32(Console.ReadLine());
            for (int i = 0; i < dataReader.FieldCount; i++)
            {
                if (dataReader.Read())
                {
                    if (Timkiem == dataReader.GetInt32(1))
                    {
                        //xóa user trong danh sach
                        string idsach = dataReader.GetString(3);
                        dataReader.Close();
                        string deleteQuery = "DELETE FROM DSMuonTra WHERE SDT =" + Timkiem;
                        SqlCommand deleteCommand = new SqlCommand(deleteQuery, conn);
                        deleteCommand.ExecuteNonQuery();
                        // Trả sách về kho
                        string displayQuery1 = "SELECT * FROM Sach";
                        SqlCommand displayCommand1 = new SqlCommand(displayQuery1, conn);
                        SqlDataReader dataReader1 = displayCommand1.ExecuteReader();
                        dataReader1.Read();
                        int soluong = (int)dataReader1.GetInt32(5);
                        dataReader1.Close();
                        string updateQuery = "UPDATE Sach SET SoLuong= " + (soluong + 1) + "WHERE IDSach =" + idsach + "";
                        SqlCommand updateCommand = new SqlCommand(updateQuery, conn);
                        updateCommand.ExecuteNonQuery();
                        conn.Close();
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("\n[✔️] Hoàn Thành !!!");
                        Console.ResetColor();
                        Console.WriteLine("══════════════════════════════════════════════════════════════");
                        GoBack();
                        break;
                    }
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine(" \n\n[❌] SDT không tồn tại !!!\n");
                    Console.ResetColor();
                    Console.WriteLine("══════════════════════════════════════════════════════════════");
                    conn.Close();
                    GoBack();
                }
            }
        }
        static void ChoMuon()
        {
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM Sach";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
            Console.WriteLine($"│{"                Chức năng mượn sách",-60}│");
            Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
            Console.Write("Nhập ID Sách Cho Mượn:");
            int Timkiem = int.Parse(Console.ReadLine());
            for (int i = 0; i < dataReader.FieldCount; i++)
            {
                if (dataReader.Read())
                {
                    
                    if (Timkiem == dataReader.GetInt32(0))
                    {
                        int soluong = (int)dataReader.GetInt32(5);
                        if (soluong > 0)
                        {
                            dataReader.Close();
                            string updateQuery = "UPDATE Sach SET SoLuong= " + (soluong - 1) + "WHERE IDSach =" + Timkiem + "";
                            SqlCommand updateCommand = new SqlCommand(updateQuery, conn);
                            updateCommand.ExecuteNonQuery();
                            Console.Write("Nhập Tên: ");
                            string tenuser = Console.ReadLine();
                            Console.Write("Nhập SDT: ");
                            int sdt = int.Parse(Console.ReadLine());
                            Console.Write("Nhập Địa Chỉ: ");
                            string diachi = Console.ReadLine();
                            Console.Write("Ngày Mượn: ");
                            DateTime ngaymuon = DateTime.Now;
                            Console.WriteLine(ngaymuon.ToString("dd/MM/yyyy"));
                            Console.Write("Ngày Trả: ");
                            DateTime ngaytra = DateTime.Parse(Console.ReadLine());
                            string insertQuery = "INSERT INTO DSMuonTra (IDsach,TenUser,SDT,DiaChi,NgayMuon,NgayTra) VALUES('" + Timkiem + "','" + tenuser + "'," + sdt + ",'" + diachi + "','" + ngaymuon.ToString("dd/MM/yyyy") + "','" + ngaytra.ToString("dd/MM/yyyy") + "')";
                            SqlCommand Insert = new SqlCommand(insertQuery, conn);
                            Insert.ExecuteNonQuery();
                            Console.ForegroundColor = ConsoleColor.Green;
                            Console.WriteLine("[✔️] Hoàn Thành !!!");
                            Console.ResetColor();
                            Console.WriteLine("══════════════════════════════════════════════════════════════");
                            conn.Close();
                            GoBack();
                            break;
                        }
                        else
                        {
                            Console.ForegroundColor = ConsoleColor.Red;
                            Console.WriteLine("[❌] Sách không đủ");
                            Console.ResetColor();
                            Console.WriteLine("══════════════════════════════════════════════════════════════");
                            conn.Close();
                            GoBack();
                        }

                    }
                    Console.ForegroundColor = ConsoleColor.Red;
                    Console.WriteLine("[❌] Sách không tồn tại");
                    Console.ResetColor();
                    Console.WriteLine("══════════════════════════════════════════════════════════════");
                    conn.Close();
                    GoBack();

                }
            }

        }
        static void TimKiem()
        {
            Console.OutputEncoding = Encoding.UTF8;
            string connString = ConnectionString;
            SqlConnection conn = new SqlConnection(connString);
            conn.Open();
            string displayQuery = "SELECT * FROM Sach";
            SqlCommand displayCommand = new SqlCommand(displayQuery, conn);
            SqlDataReader dataReader = displayCommand.ExecuteReader();
            ConsoleKeyInfo key;
            int menu = 1;
            String adu = "⤷";
            bool chon = false;
            while (!chon)
            {
                Console.WriteLine("┌——————————————————————————————————————————————————————————————┐");
                Console.WriteLine($"│{"               Chức năng tìm kiếm sách",-60}  │");
                Console.WriteLine("├——————————————————————————————————————————————————————————————┤");
                Console.WriteLine($"│{"[Menu] Các chức năng:",-62}│");
                Console.WriteLine($"│{"",-62}│");
                Console.WriteLine($"│{(menu == 1 ? adu : " ")} {"1.Tìm Sách Theo Tên",-60}│");
                Console.WriteLine($"│{(menu == 2 ? adu : " ")} {"2.Tìm Sách Theo Tác Giả",-60}│");
                Console.WriteLine($"│{(menu == 3 ? adu : " ")} {"3.Tìm Sách Thể Loại", -60}│");
                Console.WriteLine($"│{"",-62}│");
                Console.WriteLine("┗———————————————————————————————————————————————————————————-——┚");
                key = Console.ReadKey(true);
                Console.Clear();
                switch (key.Key)
                {
                    case ConsoleKey.DownArrow:
                        menu = (menu == 3 ? 1 : menu + 1 );
                        break;
                    case ConsoleKey.UpArrow:
                        menu = (menu == 1 ? 3 : menu - 1);
                        break;
                    case ConsoleKey.Enter:
                        chon = true;
                        if (menu == 1) 
                        {
                            Console.Write("Nhập Tên Sách:");
                            string Timkiem = Console.ReadLine();
                            Console.WriteLine("┌——————————┬——————————————————————————————┬————————————————————┬——————————————————————————————┬——————————┬————————┐");
                            Console.WriteLine($"│{"ID Sach",-10}│{"Tên Sách",-30}│{"Tác Giả",-20}│{"Thể Loại",-30}│{"Giá Sách",-10}│{"Số Lượng",-8}│");
                            Console.WriteLine("├——————————┼——————————————————————————————┼————————————————————┼——————————————————————————————┼——————————┼———---——┤");
                            for (int i = 0; i < dataReader.FieldCount; i++)
                            {
                                if (dataReader.Read())
                                {
                                    
                                    if (Timkiem == dataReader.GetString(1))
                                    {
                                        Console.Write($"│{dataReader.GetValue(0),-10}");
                                        Console.Write($"│{dataReader.GetValue(1),-30}");
                                        Console.Write($"│{dataReader.GetValue(2),-20}");
                                        Console.Write($"│{dataReader.GetValue(3),-30}");
                                        Console.Write($"│{dataReader.GetValue(4),-10}");
                                        Console.WriteLine($"│{dataReader.GetValue(5),-8}│");
                                        
                                    }
                                }
                            }
                            Console.WriteLine("┗——————————————————————————————————————————————————————————————————————————————————————————————————————————————-——┚");
                            dataReader.Close();
                            conn.Close();
                            GoBack();
                        }
                        if (menu == 2)
                        {
                            Console.Write("Nhập Tên Tác Giả:");
                            string Timkiem = Console.ReadLine();
                            Console.WriteLine("┌——————————┬——————————————————————————————┬————————————————————┬——————————————————————————————┬——————————┬————————┐");
                            Console.WriteLine($"│{"ID Sach",-10}│{"Tên Sách",-30}│{"Tác Giả",-20}│{"Thể Loại",-30}│{"Giá Sách",-10}│{"Số Lượng",-8}│");
                            Console.WriteLine("├——————————┼——————————————————————————————┼————————————————————┼——————————————————————————————┼——————————┼———---——┤");
                            for (int i = 0; i < dataReader.FieldCount; i++)
                            {
                                if (dataReader.Read())
                                {
                                    
                                    if (Timkiem == dataReader.GetString(2))
                                    {
                                        
                                        
                                        Console.Write($"│{dataReader.GetValue(0),-10}");
                                        Console.Write($"│{dataReader.GetValue(1),-30}");
                                        Console.Write($"│{dataReader.GetValue(2),-20}");
                                        Console.Write($"│{dataReader.GetValue(3),-30}");
                                        Console.Write($"│{dataReader.GetValue(4),-10}");
                                        Console.WriteLine($"│{dataReader.GetValue(5),-8}│");

                                        
                                    }

                                }
                            }
                            Console.WriteLine("┗—————————————————————————————————————————————————————————————————————————————————————————————————————————————————┚");
                            dataReader.Close();
                            conn.Close();
                            GoBack();
                        }
                        if (menu == 3)
                        {
                            Console.WriteLine("1.Chinh tri - Phap luat\n2.Khoa hoc - Cong nghe\n3.Kinh te\n4.Van hoc - Nghe thuat\n5.Van hoa xa hoi - Linh su\n6.Giao trinh\n7.Truyen - Tieu thuyet\n8.Tam li - Tam linh - Ton giao");
                            Console.Write("Nhập Thể Loại:");
                            string Timkiem = Console.ReadLine();
                            Console.WriteLine("┌——————————┬——————————————————————————————┬————————————————————┬——————————————————————————————┬——————————┬————————┐");
                            Console.WriteLine($"│{"ID Sach",-10}│{"Tên Sách",-30}│{"Tác Giả",-20}│{"Thể Loại",-30}│{"Giá Sách",-10}│{"Số Lượng",-8}│");
                            Console.WriteLine("├——————————┼——————————————————————————————┼————————————————————┼——————————————————————————————┼——————————┼———---——┤");
                            for (int i = 0; i < dataReader.FieldCount; i++)
                            {
                                if (dataReader.Read())
                                {
                                    
                                    if (Timkiem == dataReader.GetString(3))
                                    {
                                        Console.Write($"│{dataReader.GetValue(0),-10}");
                                        Console.Write($"│{dataReader.GetValue(1),-30}");
                                        Console.Write($"│{dataReader.GetValue(2),-20}");
                                        Console.Write($"│{dataReader.GetValue(3),-30}");
                                        Console.Write($"│{dataReader.GetValue(4),-10}");
                                        Console.WriteLine($"│{dataReader.GetValue(5),-8}│");
                                        GoBack();
                                    }
                                }
                            }
                            Console.WriteLine("┗————————————————————————————————————————————————————————————————————————————————————————————————————————————————-——┚");
                            dataReader.Close();
                            conn.Close();
                            GoBack();
                        }
                        break;
                }
            }
            
        }
        static void GoBack()
        {
            Console.OutputEncoding = Encoding.UTF8;
            ConsoleKeyInfo key;
            int menu = 1;
            String adu = "⤷";
            bool chon = false;
            while (!chon)
            {
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine($"\n\n{(menu == 1 ? adu : " ")} Enter Để Quay Lại");
                Console.ResetColor();
                key = Console.ReadKey(true);
                switch (key.Key)
                {
                    case ConsoleKey.Enter:
                        chon = true;
                        if (menu == 1) {Console.Clear();Main();}
                        break;
                }
            }
        }
        public static string ConnectionString = @"Data Source=SIINQUYET\SQLEXPRESS;Initial Catalog=SThuVien;Integrated Security=True";
        public static Random random = new Random();
        static void Main() 
        {
            Console.OutputEncoding = Encoding.UTF8;
            ConsoleKeyInfo key;
            int menu = 1;
            String adu = "⤷";
            bool chon = false;
            while (!chon)
            {
                Console.WriteLine("┌————————————————————————————————————————————————————————————┐");
                Console.WriteLine($"│{"         📖📖📖Quản Lí Sách Thư Viện📖📖📖",-60}│");
                Console.WriteLine("├—————————————————————————————————————————————————————————-——┤");
                Console.WriteLine($"│{"[Menu] Các chức năng :",-60}│");
                Console.WriteLine($"│{"",-60}│");
                Console.WriteLine($"│{(menu == 1 ? adu : " ")} {"1.Thêm sách",-58}│");
                Console.WriteLine($"│{(menu == 2 ? adu : " ")} {"2.Sách thư viên",-58}│");
                Console.WriteLine($"│{(menu == 3 ? adu : " ")} {"3.Xóa sách",-58}│");
                Console.WriteLine($"│{(menu == 4 ? adu : " ")} {"4.Chỉnh thông tin sách",-58}│");
                Console.WriteLine($"│{(menu == 5 ? adu : " ")} {"5.Tìm kiếm sách",-58}│");
                Console.WriteLine($"│{(menu == 6 ? adu : " ")} {"6.Cho mượn sách",-58}│");
                Console.WriteLine($"│{(menu == 7 ? adu : " ")} {"7.Trả sách",-58}│");
                Console.WriteLine($"│{(menu == 8 ? adu : " ")} {"8.Danh sách mượn trả",-58}│");
                Console.WriteLine($"│{"",-60}│");
                Console.WriteLine("┗————————————————————————————————————————————————————————--——┚");
                key = Console.ReadKey(true);
                Console.Clear();
                switch (key.Key)
                {
                    case ConsoleKey.DownArrow:
                        menu = ( menu == 8 ? 1 : menu + 1);
                        break;
                    case ConsoleKey.UpArrow:
                        menu = ( menu == 1 ? 8 : menu - 1);
                        break;
                    case ConsoleKey.Enter:
                        chon = true;
                        if (menu == 1) { ThemSach(); }
                        if (menu == 2) { DSSach(); }
                        if (menu == 3) { XoaSach(); }
                        if (menu == 4) { ChinhSua(); }
                        if (menu == 5) { TimKiem(); }
                        if (menu == 6) { ChoMuon(); }
                        if (menu == 7) { TraSach(); }
                        if (menu == 8) { DSMuonTra(); }
                        break;
                }
            }
            Console.ReadKey();
        }
    }
}
