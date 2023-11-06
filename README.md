import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class Cinema {

    public static class Film {

        private String titolo;
        private String genere;
        private String durata;
        private List<String> orariProiezione;

        public Film(String titolo, String genere, String durata, List<String> orariProiezione) {
            this.titolo = titolo;
            this.genere = genere;
            this.durata = durata;
            this.orariProiezione = orariProiezione;
        }

        public List<String> getOrariProiezione() {
            return orariProiezione;
        }

        public String getTitolo() {
            return titolo;
        }
    }

    public static class Sala {

        private int postiDisponibili;

        public Sala(int postiDisponibili) {
            this.postiDisponibili = postiDisponibili;
        }
    }

    public static class Prenotazione {

        private String nomeCliente;
        private Film film;
        private int nPostiPrenotati;
        private String orarioPrenotazione;
        private double prezzoBiglietto;

        public Prenotazione(String nomeCliente, Film film, int nPostiPrenotati, String orarioPrenotazione,
                double prezzoBiglietto) {
            this.nomeCliente = nomeCliente;
            this.film = film;
            this.nPostiPrenotati = nPostiPrenotati;
            this.orarioPrenotazione = orarioPrenotazione;
            this.prezzoBiglietto = prezzoBiglietto;
        }
    }

    public static void main(String[] args) {

        Scanner console = new Scanner(System.in);

        List<String> orariProiezione = new ArrayList<>();

        Film f1 = new Film("The Avengers", "Azione", "2h 23m",
                Arrays.asList("17:00", "18:30", "20:00", "21:30", "23:00"));
        Film f2 = new Film("Titanic", "Drammatico", "3h 14m", Arrays.asList("16:00", "17:00", "18:00", "19:00"));
        Film f3 = new Film("Indiana Jones 5", "Avventura", "2h 22m", Arrays.asList("20:30", "21:00", "22:30"));

        List<Film> film = new ArrayList<>();

        film.add(f1);
        film.add(f2);
        film.add(f3);

        System.out.println("Programmazione film: ");

        for (Film f : film) {
            System.out.println(f.getTitolo());
        }

        System.out.println("Scegli film: ");
        String titolo = console.nextLine();

        Film filmSelezionato = null;

        for (Film f : film) {
            if (f.getTitolo().equals(titolo)) {
                filmSelezionato = f;
                break;
            }
        }

        if (filmSelezionato != null) {

            System.out.println("Inserisci nome: ");
            String nomeCliente = console.nextLine();

            System.out.println("Inserisci il numero di biglietti: ");
            int nPostiPrenotati = console.nextInt();

            console.nextLine();

            System.out.println("Scegliere orario prenotazione: ");
            List<String> orariDisponibili = filmSelezionato.getOrariProiezione();

            for (String orario : orariDisponibili) {
                System.out.println(orario);
            }

            String orarioPrenotazione = console.nextLine();

            double prezzoBiglietto = 9.90;
            double prezzoTotale = prezzoBiglietto * nPostiPrenotati;

            Prenotazione prenotazione = new Prenotazione(nomeCliente, filmSelezionato, nPostiPrenotati,
                    orarioPrenotazione,
                    prezzoBiglietto);

            System.out.println("Prenotazione effettuata: ");
            System.out.println("Nome cliente = " + nomeCliente + ", " + "Film: " + titolo + ", "
                    + "Numero biglietti: " + nPostiPrenotati + ", " + "Orario: " + prenotazione.orarioPrenotazione
                    + ", " + "Prezzo totale: " + prezzoTotale);
        } else {
            System.out.println("Film non trovato.");
        }
    }
}
