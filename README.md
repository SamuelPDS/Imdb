# Imdbimport java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.net.http.HttpResponse.BodyHandlers;
import java.util.List;
import java.util.Map;

public class App {
    public static void main(String[] args) throws Exception {
        //HTTP - Protocolo de comunicação na Web (Request, response)
        
        //Conexão na Web por HTTP e buscar o top 250 filmes (utilizando um site disponibilizado pela alura pois o do IMDb deu acesso negado)
        String url = "https://raw.githubusercontent.com/alura-cursos/imersao-java-2-api/main/TopMovies.json";
        URI endereco = URI.create(url);
        HttpClient client = HttpClient.newHttpClient();
        var request = HttpRequest.newBuilder(endereco).GET().build();
        HttpResponse<String> response = client.send(request, BodyHandlers.ofString());
        String body = response.body();
        System.out.println(body);

        //pode ser usado o "var" no lugar do tipo de variável "HttpsClient " 

        //extrair/parciar somente dados interessados (título, poster, classificação)
        var parser = new JsonParser(); 
        List<Map<String, String>> ListaDeFilmes = parser.parse(body);
        //System.out.println(ListaDeFilmes.size());
        //System.out.println(ListaDeFilmes.get(0));

        //manipular dados 
        for (Map<String,String> filme : ListaDeFilmes) {
            System.out.println( "\u001b[1mTítulo " + filme.get("title"));
            System.out.println("\u001b[1mTítulo" + filme.get("image"));
            float rate = Float.parseFloat(filme.get("imDbRating"));
            int estrelas = (int) rate;
            System.out.println(filme.get("imDbRating"));
        
        for (int n = 1; n<=estrelas; n++) {
            
            System.out.print(":star2:");
        }       
        System.out.println("\n");
        }
        System.out.println("\n");
    }
}
