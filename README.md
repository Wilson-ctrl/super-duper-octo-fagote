# super-duper-octo-fagote
Meus primeiros passos na programação
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp4
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
  
        //vetores da implementação
        string[] Clientes = new string[10];
        string[] ContaC = new string[10];
        string[] ContaP = new string[10];
        int qtdClientes = 0, qtdContaC = 0, qtdContaP = 0;

        //==================Menu Principal=====================
        private void btnContaC_Click(object sender, EventArgs e)
        {          
            panelMenuContaC.Visible = true;//Aparecer o Menu de opções de conta corrente
        }
        private void btnContaP_Click(object sender, EventArgs e)
        {
            panelMenuContaP.Visible = true; //Aparecer o Menu de opções de conta poupança
        }
        private void btnContaE_Click(object sender, EventArgs e)
        {
            //Mensagem que indica que a opção está em desenvolvimento e volta para o MENU PRINCIPAL
            MessageBox.Show("Em desenvolvimento"); 
        }

        private void btnSair_Click(object sender, EventArgs e)
        {
            //Mensagem de despedida e encerramento do programa 
            MessageBox.Show("Programa finalizado. Até mais!"); 
            Close();
        }
        //==================Fim do Menu Principal===================

        //====================Menu de Opções Conta Corrente========================
        //Ao clicar nesse botão "abertura de conta" inicia-se o processo de aberturade conta
        private void btnAberturaDeContaC_Click(object sender, EventArgs e)
        {
            //formulário para abertura de conta corrente
            panelCadastroCliente.Visible = true; //Abre o Campo do cliente
            panelAbertContaC.Visible = true;//Abre o campo de abertura conta corrente
            listBox1.Visible = false; //fecha as listas
            listBox2.Visible = false; //fecha as listas

        }
        //Exixibr listas cadastradas
        private void btnListaContaC_Click(object sender, EventArgs e)
        {
            //Se a lista estiver conta cadastrada, exibir ela
            if (listBox1.Items.Count !=0)
            {
                listBox1.Visible = true; //Abre a  lista
                panelCadastroCliente.Visible = false; //fecha o Campo de cadastro do cliente
                panelAbertContaC.Visible = false; // fecha o campo de abertura de conta corrente
            }
            //se não tiver exibir mensagem de erro e voltar ao menu principal
            else
            {
                 MessageBox.Show("Não há conta desse tipo no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
           
        }
        //Retorna ao MENU PRINCIPAL da implementação
        private void btnMenuPrincipalC_Click(object sender, EventArgs e)
        {
            //Volta ao Menu Principal da aplicação
            panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
            panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
            panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
            panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
            panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
            listBox1.Visible = false; //fecha as listas
            listBox2.Visible = false; //fecha as listas
            return;
        }
        
        //Ao clicar na opção "ABRIR CONTA", é criado a conta corrente se todos os dados estiverem preenchidos
        private void btnAbrirContaC_Click(object sender, EventArgs e)

        {

            /*se dois CPF's iguais forem digitados exibe 
            a mensagem informando que o mesmo já é cliente*/
            if (listBox3.Items.Contains(cpfCliente.Text))
            {
                MessageBox.Show("Você já é nosso cliente");
            }
            //limite de contas correntes
            else if (qtdClientes > 9)
            {
                /*mensagem de erro, após tentar criar conta 
                 corrente com o vetor contaC estar cheio*/
                MessageBox.Show("Não estamos aceitando novos clientes no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
            //se o cliente enviar um campo vazio exibir mensagem de erro
            //impede que o usuário digite um campo vazio
            else if ((cpfCliente.Text == "") || (endCliente.Text == "") || (nomeCliente.Text == "") || (dataNascCliente.Text == "") || (agenciaContaC.Text == "") || (contaContaC.Text == "") || (saldoContaC.Text == "") || (dtAbertContaC.Text == "") || (identTitularContaC.Text == ""))
            {
                MessageBox.Show("Exite um campo vazio");
            }

            //limite de contas correntes
            else if (qtdContaC > 9)
            {
                //mensagem de alerta para avisar que esta cheio
                MessageBox.Show("Não estamos abrindo contas desse tipo no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
            else
            {
                //adicionar dados da conta corrente ao vetor de contaC
                ContaC[qtdContaC] = Convert.ToString((agenciaContaC.Text, contaContaC.Text, saldoContaC.Text, dtAbertContaC.Text, identTitularContaC.Text));
                //adicionar dados a lista
                listBox1.Items.Add(ContaC[qtdContaC]);
                qtdContaC++;

                //adiciona os dados do cliente ao vetor Clientes
                Clientes[qtdClientes] = Convert.ToString((cpfCliente.Text, nomeCliente.Text, endCliente.Text, dataNascCliente.Text));
                qtdClientes++;
                //adiciona os cpf digitado em um campo para guardá-los
                listBox3.Items.Add(cpfCliente.Text);

                MessageBox.Show("Conta Corrente aberta com sucesso!");

                //limpa os campos digitados para iniciar uma nova digitação
                cpfCliente.Clear();
                endCliente.Clear();
                nomeCliente.Clear();
                dataNascCliente.Clear();
                agenciaContaC.Clear();
                contaContaC.Clear();
                saldoContaC.Clear();
                dtAbertContaC.Clear();
                identTitularContaC.Clear();

                ///Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;

            }

        }
        //====================Fim Menu de Opções Conta Corrente======================= 
        private void btnCadastraCliente_Click(object sender, EventArgs e)
        {
    
        }
        //Fim do Cadastro de Clientes

        //====================Menu de Opções Conta poupança========================
        //Inicia-se o processo de abertura de conta poupança
        private void btnAberturaContaP_Click(object sender, EventArgs e)
        {
            //formulário para abertura de conta poupança  
            panelCadastroCliente.Visible = true; //Abre o Campo do cliente
            panelAberturaContaP.Visible = true;//Abre o campo de abertura conta poupança
            listBox1.Visible = false; //fecha as listas
            listBox2.Visible = false; //fecha as listas 

        }
        //lista da conta poupança
        private void btnListaContaP_Click(object sender, EventArgs e)
        {

            //Se a lista estiver conta cadastrada, exibir ela
            if (listBox2.Items.Count != 0)
            {
                listBox2.Visible = true;//abre a lista de conta poupança
                panelCadastroCliente.Visible = false;//fecha o campo de cadastro de cliente
                panelAberturaContaP.Visible = false;//fecha o campo de aabertura de conta poupança
            }
            //se não tiver exibir mensagem de erro e voltar ao menu principal
            else
            {
                MessageBox.Show("Não há conta desse tipo no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
        }
        // volta ao menu principal
        private void btnMenuPrincipalP_Click(object sender, EventArgs e)
        {
            //Volta ao Menu Principal da aplicação
            panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
            panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
            panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
            panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
            panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
            listBox1.Visible = false; //fecha as listas
            listBox2.Visible = false; //fecha as listas
            return;
        }
        //Abre a conta poupança
        private void btnAbrirContaP_Click(object sender, EventArgs e)
        {
            /*se dois CPF's iguais forem digitados exibe 
            a mensagem informando que o mesmo já é cliente*/
            if (listBox3.Items.Contains(cpfCliente.Text))
            {
                MessageBox.Show("Você já é nosso cliente");
            }
            
            //limite de clientes cadastrados
           else if (qtdClientes > 9)
            {
                /*mensagem de erro, após tentar criar conta 
                 corrente com o vetor Clientes esta cheio*/
                MessageBox.Show("Não estamos aceitando novos clientes no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
            //evita que o usuário informe um campo vazio
           else if ((cpfCliente.Text == "") || (endCliente.Text == "") || (nomeCliente.Text == "") || (dataNascCliente.Text == "") || (agenciaContaP.Text == "") || (contaContaP.Text == "") || (saldoContaP.Text == "") || (dtAbertContaP.Text == "") || (identTitularContaP.Text == "") || (diaVencContaP.Text == ""))
            {
                MessageBox.Show("Exite um campo vazio");
            }
            //limite da lista de conta poupança
           else if (qtdContaP > 9)
            {
                //mensagem de lotação, informando que o ambiente de cliente está cheio
                MessageBox.Show("Não estamos abrindo contas desse tipo no momento");
                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
            else
            {
                //adciona os dados da conta poupança ao vetor contaC
                ContaP[qtdContaP] = Convert.ToString((agenciaContaP.Text, contaContaP.Text, saldoContaP.Text, dtAbertContaP.Text, identTitularContaP.Text, diaVencContaP.Text, ultTaxRend.Text));
                listBox2.Items.Add(ContaP[qtdContaP]);//adiciona na lista de contas poupança
                qtdContaP++;

                //adiciona os dados do cliente ao vetor Clientes
                Clientes[qtdClientes] = Convert.ToString((cpfCliente.Text, nomeCliente.Text, endCliente.Text, dataNascCliente.Text));
                qtdClientes++;
                //adiciona os cpf digitado em um campo para guardá-los
                listBox3.Items.Add(cpfCliente.Text);

                MessageBox.Show("Conta Poupança aberta com sucesso!"); ;
                //limpa os campos digitados para iniciar uma nova digitação
                cpfCliente.Clear();
                endCliente.Clear();
                nomeCliente.Clear();
                dataNascCliente.Clear();
                agenciaContaP.Clear();
                contaContaP.Clear();
                saldoContaP.Clear();
                dtAbertContaP.Clear();
                identTitularContaP.Clear();
                diaVencContaP.Clear();

                //Volta ao Menu Principal da aplicação
                panelCadastroCliente.Visible = false;//fecha o campo de cadastrar cliente
                panelAbertContaC.Visible = false;//fecha o campo de abrir conta corrente
                panelAberturaContaP.Visible = false;//fecha o campo de abrir conta poupança
                panelMenuContaC.Visible = false;//fecha o menu de opções de conta corrente
                panelMenuContaP.Visible = false;//fecha o menu de opções de conta poupança
                listBox1.Visible = false; //fecha as listas
                listBox2.Visible = false; //fecha as listas
                return;
            }
            
        }
        //====================Fim Menu de Opções Conta poupança========================
        private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
        {

        }

        private void identTitularContaC_TextChanged(object sender, EventArgs e)
        {

        }

        private void identTitularContaP_TextChanged(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void listBox3_SelectedIndexChanged(object sender, EventArgs e)
        {

        }
        
    }
}
