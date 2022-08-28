# EditorTexto
Programa de editor de texto com Menu e os métodos de salvar, abrir e novo arquivo.


namespace EditorTexto;

internal class Program
{
    private static void Main(string[] args)
    {
        Menu();
    }
    static void Menu()
    {

        Console.Clear();
        Console.WriteLine("-------EDITOR DE TEXTO---------");
        Console.WriteLine("");
        Console.WriteLine("O que vc deseja realizar?");
        Console.WriteLine("Opção 1: Abrir arquivo.");
        Console.WriteLine("Opção 2: Novo arquivo");
        Console.WriteLine("Opção 0: Sair");
        Console.WriteLine("-------------------------------");

        short numEscolhido = short.Parse(Console.ReadLine());

        switch (numEscolhido)
        {
            case 1:; AbrirArquivo(); break;
            case 2:; NovoArquivo(); break;
            case 0: System.Environment.Exit(0); break;
            default: Menu(); break;
        }
    }

    static void AbrirArquivo()
    {
        Console.Clear();
        Console.WriteLine("-------EDITOR DE TEXTO---------");
        Console.WriteLine("");
        Console.WriteLine("Qual arquivo deseja abrir?");
        Console.WriteLine("-------------------------------");

        string path = Console.ReadLine();
        string texto = "";

        using (var file = new StreamReader(path))
        {
            string escrita = file.ReadToEnd();
            Console.WriteLine(escrita);

            do
                texto += Console.ReadLine();

            while (Console.ReadKey().Key != ConsoleKey.Escape);
        }

        Console.WriteLine("");
        Console.ReadLine();
        Salvar(texto);
        Menu();
    }

    static void NovoArquivo()
    {
        Console.Clear();
        Console.WriteLine("-------EDITOR DE TEXTO---------");
        Console.WriteLine("");
        Console.WriteLine("    DIGITE O TEXTO DESEJADO    ");
        Console.WriteLine("        (ESC para sair)        ");
        Console.WriteLine("");
        Console.WriteLine("-------------------------------");

        string texto = "";

        do
        {
            texto += Console.ReadLine();
            texto += Environment.NewLine;
        }
        while (Console.ReadKey().Key != ConsoleKey.Escape);

        Salvar(texto);
        Menu();
    }

    static void Salvar(string texto)
    {
        Console.Clear();
        Console.WriteLine("Qual caminho você deseja salvar?");
        var path = Console.ReadLine();

        using (var file = new StreamWriter(path))
        {
            file.Write(texto);
        }

        Console.WriteLine($"Arquivo {path} salvo com sucesso!");
        Console.ReadLine();
        Menu();
    }
}
