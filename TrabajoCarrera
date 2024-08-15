class Carrera {
    private static final Object testigo = new Object();
    private static final int NUM_ATLETAS = 4;
    
    public static void main(String[] args) {
        Atleta[] atletas = new Atleta[NUM_ATLETAS];
        
        for (int i = 0; i < NUM_ATLETAS; i++) {
            atletas[i] = new Atleta(i + 1);
            new Thread(atletas[i]).start();
        }
        
        synchronized (testigo) {
            testigo.notify(); // El primer atleta comienza
        }
    }
}

class Atleta implements Runnable {
    private int numero;

    public Atleta(int numero) {
        this.numero = numero;
    }

    @Override
    public void run() {
        synchronized (Carrera.testigo) {
            try {
                Carrera.testigo.wait(); // Espera su turno para correr
                long tiempoInicio = System.currentTimeMillis();
                
                Thread.sleep((long) (Math.random() * 2000 + 9000));
                
                long tiempoFin = System.currentTimeMillis();
                System.out.println("Atleta " + numero + " terminó en " + 
                    (tiempoFin - tiempoInicio) / 1000.0 + " segundos.");
                
                Carrera.testigo.notify();
                
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
