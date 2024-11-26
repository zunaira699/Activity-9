# Activity-9
using DataAccess;
using System;
using System.Data;
using System.Windows.Forms;

namespace CustomerDataEntry
{
    public partial class frmCustomerDataEntry : Form
    {
        public frmCustomerDataEntry()
        {
            InitializeComponent();
        }
        private void frmCustomerDataEntry_Load(object sender, EventArgs e)
        {
            loadCustomer();
        }
        private void loadCustomer()
        {
            try
            {
                DataSet ds = clsSqlServer.getCustomerData(); 
                dtgCustomer.DataSource = ds.Tables[0];
            }
            catch (Exception ex)
            {
                MessageBox.Show($"Error: {ex.Message}");
            }
        }
        private void btnDelete_Click(object sender, EventArgs e)
        {
            string customerName = txtName.Text;

            try
            {
                clsSqlServer.deleteCustomer(customerName); 
                MessageBox.Show("Customer deleted successfully.");
                clearForm();
                loadCustomer();
            }
            catch (Exception ex)
            {
                MessageBox.Show($"Error: {ex.Message}");
            }
        }
        private void clearForm()
        {
            txtName.Text = "";
            cmbCountry.Text = "";
            radioMale.Checked = false;
            radioFemale.Checked = false;
            chkReading.Checked = false;
            chkPainting.Checked = false;
            radioMarried.Checked = false;
            radioUnmarried.Checked = false;
        }
    }
}
