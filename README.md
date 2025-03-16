# BuscaDin-micaMAUI
CÓDIGO DA AGENDA 4 de DSI III











using System.Collections.ObjectModel;
using System.Linq;
using Microsoft.Maui.Controls;

public class Produto
{
    public string Nome { get; set; }
}

public partial class MainPage : ContentPage
{
    public ObservableCollection<Produto> Produtos { get; set; }
    private List<Produto> TodosOsProdutos;

    public MainPage()
    {
        InitializeComponent();
        
        TodosOsProdutos = new List<Produto>
        {
            new Produto { Nome = "Smartphone" },
            new Produto { Nome = "Notebook" },
            new Produto { Nome = "Tablet" },
            new Produto { Nome = "Fone de Ouvido" },
            new Produto { Nome = "Smartwatch" }
        };

        Produtos = new ObservableCollection<Produto>(TodosOsProdutos);
        BindingContext = this;
    }

    void OnSearchTextChanged(object sender, TextChangedEventArgs e)
    {
        var termo = e.NewTextValue?.ToLower() ?? string.Empty;
        var filtrados = TodosOsProdutos.Where(p => p.Nome.ToLower().Contains(termo)).ToList();

        Produtos.Clear();
        foreach (var produto in filtrados)
        {
            Produtos.Add(produto);
        }
    }
}
