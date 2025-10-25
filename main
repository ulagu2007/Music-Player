#include <bits/stdc++.h>

#include <random>
#include <dirent.h>
using namespace std;

class MusicPlayer {
public:
    static string MusicDir;
    struct musicQueue {
        string music;
        musicQueue *next;
        musicQueue *prev;
    };
    static void availableSongs();
    static void queueMusic(string music);
    static void playMusic();
};

MusicPlayer::musicQueue *head = nullptr, *tail = nullptr, *curr = nullptr, *temp = nullptr;
string MusicPlayer::MusicDir = "./Playlist";

void MusicPlayer::availableSongs() {
    DIR *dir;
    struct dirent *ent;
    if ((dir = opendir(MusicDir.c_str())) != nullptr) {
        while ((ent = readdir(dir)) != nullptr) {
            if (ent->d_name[0] != '.') {
                cout << ent->d_name << endl;
            }
        }
        closedir(dir);
    } else {
        perror("");
    }
}

void MusicPlayer::queueMusic(string music) {
    if(head != nullptr) {
        for (curr = head; curr != nullptr; curr = curr->next) {
            if (curr->music == music) {
                cout << "Music already in queue" << endl;
                return;
            }
        }
    }

    curr = new musicQueue;
    curr->music = music;
    curr->next = nullptr;
    curr->prev = nullptr;
    if (head == nullptr) {
        head = curr;
        tail = curr;
    } else {
        tail->next = curr;
        curr->prev = tail;
        tail = curr;
    }
}

void MusicPlayer::playMusic() {
    if (head == nullptr) {
        cout << "No music in queue" << endl;
    } else {
        for (curr = head; curr != nullptr; curr = curr->next) {
            cout << "Playing " << curr->music << endl;
            system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
            while (true) {
                cout << endl;
                cout << "1. Next music" << endl;
                cout << "2. Previous music" << endl;
                cout << "3. Pause music" << endl;
                cout << "4. Resume music" << endl;
                cout << "5. Shuffle music" << endl;
                cout << "6. Stop music" << endl;
                cout << "Choice: ";
                int choice;
                int n = rand() % 10;
                cin >> choice;
                switch (choice) {
                    case 1:
                        if (curr->next == nullptr) {
                            cout << "No next music" << endl;
                        } else {
                            curr = curr->next;
                            cout << "Playing " << curr->music << endl;
                            system("pkill mpg123");
                            system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
                        }
                        break;
                    case 2:
                        if (curr->prev == nullptr) {
                            cout << "No previous music" << endl;
                        } else {
                            curr = curr->prev;
                            cout << "Playing " << curr->music << endl;
                            system("pkill mpg123");
                            system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
                        }
                        break;
                    case 3:
                        system("pkill -STOP mpg123");
                        break;
                    case 4:
                        system("pkill -CONT mpg123");
                        break;
                    case 5:
                        for (int i = 0; i < n; i++) {
                            if (curr->next == nullptr) {
                                curr = head;
                            } else {
                                curr = curr->next;
                            }
                        }
                        cout << "Playing " << curr->music << endl;
                        system("pkill mpg123");
                        system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
                        break;
                    case 6:
                        system("pkill mpg123");
                        exit(0);
                        break;
                    default:
                        cout << "Invalid choice" << endl;
                }
            }
        }
    }
}


int main() {
    MusicPlayer mp;
    int choice;
    string music;

    cout<<"Available songs: "<<endl;
    mp.availableSongs();
    cout<<endl;

    while (true) {
        cout << "1. Queue music" << endl;
        cout << "2. Play music" << endl;
        cout << "3. Exit" << endl;
        cout << "Choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Music: ";
                cin >> music;
                mp.queueMusic(music);
                break;
            case 2:
                mp.playMusic();
                break;
            case 3:
                exit(0);
            default:
                cout << "Invalid choice" << endl;
        }
    }
}
