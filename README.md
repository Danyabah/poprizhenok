# консоль диспетчера пакетов
Scaffold-DbContext 'Server=DESKTOP-URICGBM\SQLEXPRESS;Database=Tour;Trusted_Connection=True;' Microsoft.EntityFrameworkCore.SqlServer
# entityCore + (Tools,SqlServer)
#googs.wsr.ru login + password
# connection string
"Data Source=gogs.wsr.ru;Initial Catalog=Popryzhenok;User ID=190-20;Password=8XBEkuQX;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False;App=EntityFramework"
# Логин
public int user { get; set; }
private void button1_Click(object sender, EventArgs e)
{
    using (var db = new PARFUMEContext())
    {
        if (db.Users.Any(x=>x.UserName == textBox1.Text && x.Pass == textBox2.Text)) {

            var cur = db.Users.FirstOrDefault(x => x.UserName == textBox1.Text && x.Pass == textBox2.Text);
            var main = new Form2();

            switch (cur.RoleId)
            {
                case 1:
                    user = 1;
                    MessageBox.Show("NS fdkshgf;ds");
                    break;
                case 2:
                    user = 2;
                    MessageBox.Show("Ngfdgfdgd");
                    break;
                case 3:
                    user = 3;
                    MessageBox.Show("Ngfdgfdgdfgdfdgd");
                    break;

            }
            main.Show();
        }
        else
        {
            MessageBox.Show("YFPGPODSJ");
        }
    }
}
# userControl
public UserControl1(Product product)
{
    InitializeComponent();
    this.product = product;   
    Init(product);
}
public Product product { get; set; }
public void Init(Product product)
{
    using (var db = new PARFUMEContext())
    {
        label1.Text = product.Descrip;
        label2.Text = product.Category.Title;
        label5.Text = product.Sale.ToString();

        if(product.Logo != "") 
        { 
           var path = "C:\\Users\\Alex_Sh\\source\\repos\\poh\\poh\\Resources\\" + product.Logo;
            pictureBox1.Image = Image.FromFile(path);
        }
    }
}
# formLayout

public Form2()
{
    InitializeComponent();
    Load();
}

public void Load()
{
    using (var db = new PARFUMEContext())
    {
        var products = db.Products.Include(nameof(Product.Category));
        foreach (var product in products)
        {
            var uc = new UserControl1(product);
            uc.Parent = flowLayoutPanel1;
        }

    }
}

private void textBox1_TextChanged(object sender, EventArgs e)
{
    Filter();
}

private void Filter()
{

    foreach (var item in flowLayoutPanel1.Controls)
    {
        var visible = true;

        if (item is UserControl1 uc)
        {
            if (!string.IsNullOrWhiteSpace(textBox1.Text)
                && !uc.product.Descrip.Contains(textBox1.Text))
            {
                visible = false;
            }
            uc.Visible = visible;
        }

    }

}
# БД
CREATE TABLE Products(
 id int identity (1,1) not null,
 productName nvarchar(80),
 productTypeId int,
 articul int,
 peopCount int,
 numCeh int,
 minPrice int,
 PRIMARY KEY (id), 
 FOREIGN KEY (productTypeId) REFERENCES ProductType(id) 
)
UPDATE [ProductOfAgents] SET [idAgent] = (SELECT Agents.id FROM Agents WHERE Agents.agentName = ProductOfAgents.idAgent)
