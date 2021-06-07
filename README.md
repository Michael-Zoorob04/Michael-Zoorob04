using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace TikTakToe
{
    public partial class Form1 : Form
    {
        bool turn = true; //True means its X's turn, and false means its O turn.
        int turn_count = 0;


        public Form1()
        {
            InitializeComponent();
        }

        private void NewGameToolStripMenuItem_Click(object sender, EventArgs e)
        {

        }

        private void ExitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        private void Button_click(object sender, EventArgs e)
        {
            Button b = (Button)sender;
            if (turn)
                b.Text = "X";
            else
                b.Text = "O";

            turn = !turn;
            b.Enabled = false;
            turn_count++;
            CheckForWinner();
        }

        private void CheckForWinner()
        {
            bool there_is_a_winner = false;

            //This is to check for the horizontol row.
            if ((A1.Text == A1.Text) && (A2.Text == A3.Text))
                there_is_a_winner = true;

            else if ((b1.Text == b2.Text) && (b2.Text == b3.Text))
                there_is_a_winner = true;

            else if ((C1.Text == C2.Text) && (C2.Text == C3.Text))
                there_is_a_winner = true;

            //This is to check for the vertical row
            else if ((A1.Text == b1.Text) && (b1.Text == C1.Text))
                there_is_a_winner = true;

            else if ((A2.Text == b2.Text) && (b2.Text == C2.Text))
                there_is_a_winner = true;

            else if ((A3.Text == b3.Text) && (b3.Text == C3.Text))
                there_is_a_winner = true;

            //This is to check for the diagonal row.
            else if ((A1.Text == b2.Text) && (b2.Text == C3.Text))
                there_is_a_winner = true;

            else if ((A3.Text == b2.Text) && (b2.Text == C1.Text))
                there_is_a_winner = true;

            if (there_is_a_winner)
            {
                DisableButtons();

                String winner = "";
                if (turn)
                    winner = "O";
                else
                    winner = "X";

                MessageBox.Show(winner + " Wins!", "Yipee!!");

            }
            else
            {
                if(turn_count == 9)
                    MessageBox.Show(" Draw", "That's sad");
            }

        }

        private void DisableButtons()

        {
            try
            {
                foreach (Control c in Controls)
                {
                    Button b = (Button)c;
                    b.Enabled = false;

                }
            }
            catch { }
        }
         private void newGameToolStripMenuItem_Click(object sender, EventArgs e)
        {
            turn = true;
            turn_count = 0;

            try
            {
                foreach (Control c in Controls)
                {
                    Button b = (Button)c;
                    b.Enabled = true;
                    b.Text = "";
                }
            }
            catch { }
        }
    }
}

